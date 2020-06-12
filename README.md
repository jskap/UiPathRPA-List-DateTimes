# UiPathRPA-List-DateTimes
Verify if the dates in the list have passed in the current year.

Given an input list of strings in format dd.MM.yyyy, please check if any of the dates has the same month as current month and print that date to output. 

For the dates having a different month, print to output the number of days that passed/due from the current date to date from list (in the current year).

Note: Initialize a list with the following value: new List(of String) from {"01.02.1980", "04.05.1985","06.08.1988","24.09.1999","18.11.1986","11.10.1983"}

In UiPath Studio, create a new project and use the following steps:

Use a 'ForEach' activity inside a sequence to iterate through all items in the list ('ForEach item in variablename') and use the following activities and methods in the Body:

 1. Create a DateTime variable ("TmpDate") and use the 'DateTime.ParseExact' method within an 'Assign' activity to convert to DateTime: TmpDate = DateTime.ParseExact(InputDate, "dd.MM.yyyy", nothing)
 
 2. Use an 'If' activity to verify if the item's month is the same with the current month: TmpDate.Month = DateTime.Now.Month:
    -- If the condition is met, print a message using the 'Write Line' activity and the 'String.Format' method.
    -- If the condition is not met, add a sequence with the following activities and methods: 
    
       a. Create a new variable of TimeSpan type ("TimeDifference") calculate the difference between the current month and the item's month using the 'Subtract' method in an 'Assign' activity: TimeDifference = Datetime.Now.Subtract(new DateTime(Datetime.Now.Year, TmpDate.Month, TmpDate.Day))
       
       b. Use an 'If' activity to verify if the date is in the future or in the past, by stating the condition as TimeDifference.Days > 0 and print a different message for when the month has passed or is in the future using the 'String.Format' method in a 'Write Line' activity: String.Format( "{0} days until the date {1}", Math.Abs(TimeDifference.Days).ToString, TmpDate.Day.ToString+ "." + TmpDate.Month.ToString+"."+DateTime.Now.Year.ToString
 
