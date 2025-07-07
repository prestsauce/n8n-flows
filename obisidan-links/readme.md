# Obsidian Links to Karakeep Workflow

This n8n workflow automates the process of extracting external links from your recently modified Obsidian notes and saving them to Karakeep.

## How it Works

1.  **Schedule Trigger**: The workflow runs on a schedule (e.g., every hour - currently set to every 30 minutes).
2.  **Get Date Parameters**: It calculates the current month's path for your Obsidian notes and a timestamp for filtering files modified within the last 30 minutes.
3.  **Get Modified Files**: It uses a shell command (`find`) to locate all files within your Obsidian vault's current month directory that have been modified in the last 30 minutes.
    * **Important**: You'll need to set the `local_path` environment variable in your n8n instance to the root directory of your Obsidian vault.
4.  **Parse File Paths**: The output from the command is parsed to get individual file paths.
5.  **Read Files from Disk**: Each identified file is read from your local disk.
6.  **Extract from File**: The content of each file is extracted.
7.  **Extract External Links**: It then extracts all external URLs (http/https links) found within the content of your notes.
8.  **Conditional Link Check**:
    * **If links are found**: It checks if the extracted link already exists in your Karakeep instance.
    * **If link does not exist in Karakeep**: The link is then posted to your Karakeep instance.
    * **Important**: You'll need to set the `karakeep_url` and `api_key` environment variables in your n8n instance for Karakeep integration.

## Setup

1.  **Download the .json file**: Import this workflow into your n8n instance.
2.  **Environment Variables**: Set the following environment variables in your n8n instance:
    * `local_path`: The absolute path to your Obsidian vault.
    * `karakeep_url`: The URL of your Karakeep instance (e.g., `http://localhost:8000`).
    * `api_key`: Your Karakeep API key.
3.  **Activate the Workflow**: Once configured, activate the workflow in n8n.

This workflow helps ensure that external resources you link in your Obsidian notes are automatically saved to your Karakeep bookmark manager, keeping your research and links organized.