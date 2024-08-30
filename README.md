
# Project: Identifying Privacy Concerns of VR Users 

This project aims to identify and categorize the privacy concerns of Virtual Reality (VR) users based on data from various online platforms, including Reddit, Discord, and Steam. The project involves data collection, preprocessing, topic identification, and clustering of user comments.

### Data Collection

Data is collected from the following platforms:

- Reddit (via the Reddit API)
- Discord (via the Discord API)
- Steam (via a Selenium-based web crawler)

The APIs provide efficient access to a vast amount of user-generated content. The web crawler automates the process of navigating Steam discussion forums and scraping relevant user comments.

### Preprocessing

The collected comments undergo preprocessing to ensure they are in a suitable format for analysis. The process includes filtering for unique comments with a length ranging from a minimum of 5 characters to a maximum of 3000 characters.

### Topic Identification

The preprocessed comments are analyzed using a GPT-3.5-powered API model. The model identifies whether each comment is concerned with VR privacy. If a comment is identified as privacy-related, the model further analyzes it to identify prominent themes and extracts quotational evidence from the comments to support these themes.

### Clustering

The comments are grouped using the AgglomerativeClustering model. The feature matrix is computed using the Term Frequency-Inverse Document Frequency (TF-IDF) measure. The cosine similarity measure is then used to calculate the similarity between documents. This precomputed cosine similarity matrix is used as input to the AgglomerativeClustering model, which groups together comments with semantic similarities.

This project provides insights into the range of privacy-related topics that VR users discuss across various online platforms, offering a rich understanding of user concerns and discussions related to VR privacy.

## How to Use

### Reddit Crawler

This script will collect posts from the subreddit you specify and save them to a CSV file. It collects the title, content, comment, comment URL, and date for each post. Make sure to replace 'YOUR_CLIENT_ID', 'YOUR_CLIENT_SECRET', 'YOUR_USER_AGENT_NAME', 'YOUR_REDDIT_USERNAME', 'YOUR_REDDIT_PASSWORD', 'YOUR_SUBREDDIT_NAME', and 'YOUR_FILE_NAME.csv' with your actual details.

Here is where you can acquire said details: https://www.reddit.com/prefs/apps

### Discord Crawler

To use this crawler, you'll need to replace placeholder values with your actual values. These include your Discord token in the headers dictionary and your channel ID in the retrieve_messages function call. You will also need to replace the CSV file name in the open function call with the desired name for your output file.

The channel Id is the last set of digits following the "/" of a url of the channel

Additionally, you will need to retrieve your authorization token: 

- Open Discord in your web browser (not the application). Log in to your account if necessary.
- Open Developer Tools:
  - For Windows users, you can press Ctrl + Shift + I.
  - For Mac users, you can press Cmd + Option + I.
  - Alternatively, you can right-click anywhere on the page, select "Inspect" (or "Inspect Element") from the dropdown menu, and then click on the "Network" tab.
- Refresh the page (press F5 or Cmd + R).
- In the "Network" tab of the Developer Tools, there will be a lot of entries. In the "Filter" field at the top, type "/api", which will help narrow down the entries.
- Click on any entry in the Name column that begins with "library".
- On the right side, click on the "Headers" tab if not already selected.
- Scroll down until you see "authorization:" in the "Request Headers" section. The alphanumeric string following "authorization:" is your token.

### Steam Crawler

To use the Steam crawler, copy the forum link that you would like to scrape. Then make sure to get the HTML tag for the "next" button for that forum to go through the various topic pages. It is different for each forum.

### GPT-3.5 Model

Once you feed your preprocessed CSV file of user comments, set the variable "file" to whatever name the CSV is, without the ".csv". It will then call unique queries to the model regarding each comment and determine what concerns of virtual reality privacy are affiliated with the comment. It will create a folder with the name of the value you assigned to "file". Within that folder will be a CSV called "ThemesandQuotevirtualreality".

### Clustering

To cluster all the comments semantically, give the parent folder path to "directory" and it will iterate through each "ThemesandQuotevirtualreality" CSV file to cluster based on cosine similarity.
