# Gazprom-Analytical-Task
I was given a worksheet table as input: "Task Uploads," "Normative Deadlines," and "Average Deadlines by Business Solution."

# Realization

I solved the problem of calculating the date of realization of the task as follows:
1. For each individual business decision, based on the issued regulatory
deadlines were calculated for the remaining deadlines after each phase. (Worksheet.
No. 3 - Average timelines for BRs).
2. In the main worksheet with the upload, the start-up implementation date was determined by
I defined the start date as "Start date + the corresponding number for each individual
business solution and project phases, the number of days required for
execution": I implemented this with the VLOOKUP function: =[@[Scheduled
exit date from current status]]+VRP([@[Business Decision]];'Average
BR dates'!$A$1:$T$203; 16).
3. The same thing was done with the implementation date with the current status,
the only thing was that for each ALREADY ongoing stage, the UPP function took the
the next. In other words, if item #2 took a value from
Extension column, I would take "Implemented" in this item.
4. I implemented the amount of overdue by a condition (if the date with the current status
more than start date is true" and the usual mathematical difference:
=If([@[Date Implemented with current status]]>[@[Date Implemented on
start]];[@[Implementation date with current status]]-[@[Implementation date at start
Start Date]];"-"). The result is the number of days, rounded to plus integers.
5. Business Decisions missing on Sheet #3 were not filled in.
6. Projects with statuses "Closed", "Rejected" were not filled in.
7. It is important that this calculation does not take into account weekly weekends, because
the problem did not formulate whether they were included in the normative /
average terms. At any rate, this aspect is easily solved
By dividing another VRP function by 7 (days in one week) and
by multiplying by 2 (two days off in one week).

# Analytics

As an analytical tool, I used Python with
Pandas data analysis library. I converted the finished .xlsx file into
.csv format (UTF-8 encoding), read it with the Pandas library, and removed all
empty lines and lines with text values. This tool
allows you to easily and very quickly get a visual mathematical
view of the data being analyzed. I examined the "Overdue" column -
2451 projects out of 3881 (63%) are overdue.

![image](https://user-images.githubusercontent.com/65823336/217369627-767a3b8f-4791-48da-8d3f-a47518787b71.png)


# BI tools

As a platform for data visualization, I chose the free
Power BI Desktop interface. Below you will find several dashboards
(dashboard) on the most significant, in my opinion, information for
for further decision making. I have selected separately for consideration: those
business solutions (by the number of projects) that have the most
overdue; the most overdue projects by planned date of execution from
current implementation.

![image](https://user-images.githubusercontent.com/65823336/217369667-f95e526e-9358-4558-ae53-672761fa7eff.png)


# To sum up

The most "problematic" business solutions in terms of the number of
of overdue projects were: OFERTA - 432 projects, ERP_KFSCH - 185
projects and KSHD - 144 projects; by the number of overdue projects: SHAHMATKA - 1,229
days, OFERTA - 602 projects and ZUP - 585 projects.
