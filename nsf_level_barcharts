# These packages are required. If you haven't already, you'll need to install them first.
# To install a package, use install.packages("packageName"). For example, to install ggplot2,
# use install.packages("ggplot2"). Then you can use library(ggplot2) to access it in any R session.
library(ggplot2)
library(gridExtra)
library(grid)
library(scales)
# Storing the names of all the columns in the report (available on OBIEE). This isn't a necessary step,
# but it can help prevent issues on the reading step so I like to use it.
columns <-
    c(
        "Overdue.Status",
        "Submission.Status",
        "Program.Element",
        "Dir",
        "Div",
        "Award.Number",
        "Award.Title",
        "Program.Officer",
        "Principal.Investigator",
        "PI.Email",
        "PI.ID",
        "Institution.Name",
        "Institution.ID",
        "Reporty.Type",
        "Report.Due.Date",
        "Report.Overdue.Date",
        "Program.Element.Code",
        "Start.Date",
        "End.Date"
    )
# read the data -- saved as a csv file -- into a dataframe assign the information to the
# variable 'rpts'
rpts <-
    read.csv("Detailed Report.csv",
             col.names = columns,
             header = TRUE)
levels(rpts$Overdue.Status) <-
    c(
        "Due 0 - 45 Days",
        "Due 46 - 90 Days",
        "Due > 90 days",
        "Overdue 1 - 45 Days",
        "Overdue 46 - 90 Days",
        "Overdue > 90 days"
    )

# First we want to create an NSF-wide plot that shows how many project reports
# are due and overdue. Start by creating the base plot usint the rpts data and
# telling it the Overdue.Status will be our x-axis data
plt <- ggplot(rpts, aes(x = Overdue.Status))
plt + geom_bar(aes(fill = Submission.Status)) +
    ggtitle("NSF Project Reports: Number of Days Due/Overdue by Submission Status")
# The NSF-wide barchart motivates the question of how the reports are distrubuted
# accross directorates. Adding facet_wrap -- which subsets the plot and displays
# the subset plots in a grid -- does just that
plt + geom_bar(aes(fill = Submission.Status)) +
    ggtitle("NSF Project Reports: Number of Days Due/Overdue by Submission Status") +
    facet_wrap(~ Dir, ncol = 2)

# Next I want to drop the IRM reports. If you want to see how many reports you're dropping,
# The command below displays each division/directorate's counts in a table
#table(rpts$Dir, rpts$Div)
# 'Subset' takes the dataframe and returns the observations that meet the condition provided
# In this case, that the 'Dir' column doesn't equal "IRM"
rpts <- droplevels(subset(rpts, rpts$Dir != "IRM"))

