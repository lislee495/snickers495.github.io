---
layout: post
title:      "Creating a Dynamic Calendar in Rails "
date:       2018-01-13 17:51:56 +0000
permalink:  creating_a_dynamic_calendar_in_rails
---


While I was creating a calendar-based app for my Ruby on Rails project, I ran into a few stumbling blocks. First, I knew I wanted to create my own calendars, which would receive events from my own Event model. I didn't want to use Google Calendar API, because I would be stuck using the app on their terms, with limited ability to customize the code. Second, I knew I wanted to have more than just a month view, because actual users would expect to switch between looking at their week, month, and day for events. So I needed a calendar model that was flexible enough to be able to make three different types of calendars. 

Luckily, I ran into the website, Rich on Rails, that had a month-calendar model similar to what I was looking for. At first, the code didn't make sense to me, because so many of the terms were new. But after getting the month calendar to work, I began to parse through the code to see what was going on. After figuring out what each component did, I was then able to customize the code to create a dynamic week calendar and day calendar with hours. This blog post will guide readers through my step-by-step process, so that they too can create a calendar customizable for their needs. 

## Calendar Components
At the heart of it, a calendar is a table. In HTML, tables look like this: 
```
<table>
 <tr>
   <th>This</th>
   <th>is</th>
 </tr>
 <tr>
   <td>a</td>
   <td>table</td>
 </tr>
</table>
```
<tr> marks a table row, which is every row of the table. <th> is the table header, where the headings go. <td> marks the cells that contain the appropriate data. A monthly calendar is just a table with weekdays as a heading, weeks as rows, and dates as cells. A weekly calendar is that except it just shows one row. 

In Ruby, it's tempting to hard code this, but this doesn't account for the changing dates that might begin one calendar's Sunday and might end on one calendar's Saturday. So we can make a dynamic calendar with the use of certain TagHelpers, which come with Ruby. With these tag helpers, we can make headers, rows, and cells based off of the information we feed them. 

## Base Code
This is the code for the model: 
```class Calendar < Struct.new(:view, :date, :callback)
    HEADER = %w[Sunday Monday Tuesday Wednesday Thursday Friday Saturday]
    START_DAY = :sunday

    delegate :content_tag, to: :view

    def table
      content_tag :table, class: "calendar table table-bordered table-striped" do
        header + week_rows
      end
    end

    def header
      content_tag :tr do
        HEADER.map { |day| content_tag :th, day }.join.html_safe
      end
    end

    def week_rows
      weeks.map do |week|
        content_tag :tr do
          week.map { |day| day_cell(day) }.join.html_safe
        end
      end.join.html_safe
    end

    def day_cell(day)
      content_tag :td, view.capture(day, &callback), class: day_classes(day)
    end

    def day_classes(day)
      classes = []
      classes << "today" if day == Date.today
      classes << "not-month" if day.month != date.month
      classes.empty? ? nil : classes.join(" ")
    end

    def weeks
      first = date.beginning_of_month.beginning_of_week(START_DAY)
      last = date.end_of_month.end_of_week(START_DAY)
      (first..last).to_a.in_groups_of(7)
    end
end```

This is the code for the CalendarHelper: 
```
module CalendarHelper
  def calendar(date = Date.today, &block)
    Calendar.new(self, date, block).table
  end
end
```

And this is the code for the Calendar view: 
```
<div class="row">
  <div class="col-md-12 text-center">
    <div class="well controls">
      <%= link_to calendar_path(date: @date - 1.month), class: "btn btn-default" do %>
        <i class="glyphicon glyphicon-backward"></i>
      <% end %>
      <%= "#{@date.strftime("%B")} #{@date.year}" %>
      <%= link_to calendar_path(date: @date + 1.month), class: "btn btn-default" do %>
        <i class="glyphicon glyphicon-forward"></i>
      <% end %>
    </div>
  </div>
</div>
<div class="row">
  <div class="col-md-12">
    <%= calendar @date do |date| %>
      <%= date.day %>
    <% end %>
  </div>
</div>
```
## Parsing through the Code
While this seems like a lot of code, it's actually pretty intuitive after a little while. To begin, let's first focus on the model code. 
```class Calendar < Struct.new(:view, :date, :callback)```

Struct isn't something I saw while I was working in Ruby, but it's apparently a built-in class that makes a model-like class, but with a few shortcuts if the developer doesn't need an actual class. For now let's skip down. 

```HEADER = %w[Sunday Monday Tuesday Wednesday Thursday Friday Saturday]
    START_DAY = :sunday```
		
The next code makes the variables for the header and start day. Obviously, if you want to make a four-day calendar, or a day calendar, this is where you would change the header. For the month and the week calendar, this header works fine. Next: 

		```def table
      content_tag :table, class: "calendar table table-bordered table-striped" do
        header + week_rows
      end
    end```
		
Here, we get the table method, which uses the content_tag helper to make a table with the class "calendar table table-bordered table-striped" and it contains the header(another method below) and the week_rows(another method) below. In terms of specificity, the general structure of this Calendar class looks like an inverted pyramid, going from most general to most specific. Let's take a look at the header method. 

```def header
      content_tag :tr do
        HEADER.map { |day| content_tag :th, day }.join.html_safe
      end
    end```
		
The header method wraps the header variable in the content tag <tr>, and maps out the header array so that each day in the header is given the content tag <th>. It joins it back, and marks it as safe with the .html_safe. The next method, week_rows, calls upon two methods we haven't looked at yet, so in order to understand that, let's first look at the methods called in it, weeks and day_cell(). 
	
	```def weeks
      first = date.beginning_of_month.beginning_of_week(START_DAY)
      last = date.end_of_month.end_of_week(START_DAY)
      (first..last).to_a.in_groups_of(7)
    end
		

For me,

		
		


