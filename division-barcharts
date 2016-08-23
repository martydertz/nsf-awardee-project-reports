# Store the working directory so it can be switched back after each
# iteration of the for loop
wd <- getwd()

for (d in levels(rpts$Dir)) {
    # reset the working directory
    setwd(wd)
    # create a name for a new folder -- the 'gsub' function will take "/" out of "O/D" which would
    # throw an error if used to create a file path
    pathName = gsub("/", "", paste0(d, "_Plots"))
    dir.create(pathName)
    # concatenate the current directory's name with the name of the file just created
    path <- paste0(wd, "/", pathName)
    # switch the working directory to the Directorate file just created
    setwd(path)
    # create a subset dataframe with only the reports for the current Directorate
    df <- droplevels(rpts[rpts$Dir == d, ])
    # for all divisions in the current directorate's dataframe...
    for (div in levels(df$Div)) {
        df2 <- droplevels(subset(df, df$Div == div))
        chartTitle <-
            paste0(div,
                   " Project Report Statuses: Counts for Each Program Officer")
        p <- ggplot(df2, aes(x = Overdue.Status))
        plt <-
            p + geom_bar(aes(fill = Submission.Status)) + ggtitle(chartTitle) +
            facet_wrap( ~ Program.Officer, ncol = 2)
        imageName <- paste0(div, "plots.png")
        jpeg(imageName, width = 1500)
        print(plt)
        dev.off()
    }
}
