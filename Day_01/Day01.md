## Day 1

    data <- read.delim("input.txt", sep="\n", header = FALSE)

This report indicates that, scanning outward from the submarine, the
sonar sweep found depths of 199, 200, 208, 210, and so on.

The first order of business is to figure out how quickly the depth
increases, just so you know what you’re dealing with - you never know if
the keys will get carried into deeper water by an ocean current or a
fish or something.

To do this, count the number of times a depth measurement increases from
the previous measurement. (There is no measurement before the first
measurement.) In the example above, the changes are as follows:

199 (N/A - no previous measurement) 200 (increased) 208 (increased) 210
(increased) 200 (decreased) 207 (increased) 240 (increased) 269
(increased) 260 (decreased) 263 (increased) In this example, there are 7
measurements that are larger than the previous measurement.

How many measurements are larger than the previous measurement?

    # iterate over each row, write if/else condition for each row, add as new text in column, count number of occurences

    # Create new column
    data <- tibble(data, "change" = character(1:length(data)))

    for (i in 2:nrow(data)-1) { # dont to it for the first or last row
      
      # Subtract next row value from current row
      curr_value <- data$V1[i+1] - data$V1[i]
      
      # Use sign to check if value is -, + or 0
      sign_curr_value <- sign(curr_value)
      
      if (sign_curr_value == 1){ data$change[i+1] <- "increased"  }   # increase
      else if (sign_curr_value == -1) {data$change[i+1] <- "decreased" }   # decrease
      else if (sign_curr_value == 0){data$change[i+1] <- "unchanged" } # stayed the same
      else { break }
      
      
    }


    # Count number of increases / decreases

    no <- table(data$change)

number of increases / decreases: 1, 418, 1581
