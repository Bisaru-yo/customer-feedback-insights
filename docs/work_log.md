Day 1
I created five empty folders in my repo, edited contents in README file, I couldn't add .gitignore in the repo at first so I had to add one later; however, I ended up creating a text file so I later on changed that to .gitignore. Up until here, I learned whole lot of git commands to do all this, while creating files I need to watch out for its extension, learned the purpose of having .gitignore.

Day 2
You created the bucket in us-east-2 because that was the only region available to you.

Using “Add folder” in the upload created doubled paths, which you fixed with aws s3 mv.

A dry run printed nothing because the path had an extra reviews/. Your count checks (70 objects, 8,128,800 bytes) proved the fix worked.



I ran a python code in databricks to check if it can touch Snowflake, AWS S3 and Anthropic API or not. It was just a test and I was surprised that it made

connection with my Claude anthropic without credentials. This was just a network test and it passed, that's  a difference between a network test and an authenticated call.



\## Day 2, Block 1: First look at the data

\*\*What I did:\*\* Opened one review file and one ticket file and compared them with the data dictionary.

\*\*What I found:\*\* The dictionary was out of date. Reviews are a JSON array, not JSON Lines. Review text has HTML. Some customer\_id and product\_id values are missing even though the dictionary says always present. Ticket dates use at least two formats. Ticket text includes quoted email replies.

\*\*Lesson:\*\* Trust the data, not the documentation. This was a sample of 1 day and 1 week, so every number needs checking across all files.



\## Day 2, Block 2: Profiling the full dataset

\*\*What I did:\*\* Loaded all 56 review files and 8 ticket files and measured duplicates, missing values, date formats, text problems, and broken links.

\*\*What I found:\*\* 8.9% repeated review rows, 2.8% repeated tickets, three ticket date formats, one review file with text ratings, one ticket file with reordered columns, HTML in 6.6% of reviews, signatures and quoted replies in about 20% of tickets each.

\*\*What went wrong:\*\* The loader failed with "No objects to concatenate" because my base path was wrong. glob returned zero files. I added an assert on the file count so it fails loudly.

\*\*Lesson:\*\* Profile per file, not just the combined table. Column order and type differences disappear once files are merged.

