#!/bin/bash

# Ensure you have jq installed: sudo apt install jq
# Replace YOUR_GITHUB_TOKEN with your actual GitHub personal access token.
# Replace ORGANIZATION_NAME with the name of the GitHub organization.

GITHUB_API="https://api.github.com"
ORGANIZATION_NAME="YOUR_ORG_NAME"
GITHUB_TOKEN="YOUR_GITHUB_TOKEN"

# Get users in the organization
get_org_users() {
    page=1
    while true; do
        response=$(curl -s -H "Authorization: token $GITHUB_TOKEN" \
                        "$GITHUB_API/orgs/$ORGANIZATION_NAME/members?per_page=100&page=$page")
        
        # Check if the response is empty (end of pages)
        if [[ $(echo "$response" | jq length) -eq 0 ]]; then
            break
        fi

        # Extract and print the login names of the users
        echo "$response" | jq -r '.[].login'

        # Move to the next page
        ((page++))
    done
}

# Call the function
get_org_users
