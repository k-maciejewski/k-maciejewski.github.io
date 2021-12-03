---
title: About
---

# Advent-of-Code-2021

About my method to read in descriptions and data for Advent of Code 2021

(Using R)

library(rvest)

library(httr)

**1. Read the description for part 1, where N is the day number**

    `r read_html("https://adventofcode.com/2021/day/N") %>% 
      html_element(".day-desc") %>% 
      paste(collapse = '\n') `
  
**2. To load data file, you need your cookie information**

Login with OAuth, then find your cookie information. (Ex: inspect element > network > input (may need to refresh) > scroll to cookies)

![](/AOC_GET.png)

Save in separate file (I used .csv) or enter in specified places below:

`input` will scrape the data for part 1

    input <- GET("https://adventofcode.com/2021/day/N/input", 
               set_cookies(`_ga`=cookie$Input[1], 
                             `_gid`=cookie$Input[2],
                             `session`=cookie$Input[3]))

**3. This is an example of how to read in and parse the data:**

    input_text <- content(input, "text") %>% 
      read_lines() %>% 
      as.array() 
  
**4. After solving part 1 and entering answer on adventofcode.com, you can read description for part 2 using the following:**  
  
    `r read_html(part2)%>% 
      html_element(".day-success+ .day-desc") %>% 
      paste(collapse = '\n')`
