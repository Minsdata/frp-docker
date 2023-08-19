#!/bin/bash

# Set your GitHub repository details
GITHUB_USER="your-github-username"
REPO_NAME="your-repo-name"
BRANCH_NAME="main"  # Set the desired branch name
FILE_PATH="path/to/yourfile.md"  # Set the desired file path in the repository
FILE_CONTENT=$(curl -s https://raw.githubusercontent.com/fatedier/frp/dev/Release.md)  # Set the external link content as the file content

# Encode the file content in base64
ENCODED_CONTENT=$(echo -n "$FILE_CONTENT" | base64)

# Create the file using GitHub API
curl -X PUT "https://api.github.com/repos/$GITHUB_USER/$REPO_NAME/contents/$FILE_PATH" \
  -H "Authorization: token YOUR_GITHUB_TOKEN" \
  -d '{
    "message": "Create file",
    "branch": "'$BRANCH_NAME'",
    "content": "'$ENCODED_CONTENT'",
    "committer": {
      "name": "Your Name",
      "email": "your@email.com"
    }
  }'
