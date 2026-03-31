# AI-Agent-to-Automatically-Create-Videos-and-Post-Them-on-Social-Media-N8N

An advanced **n8n AI content automation workflow** that generates viral short-form video ideas, creates AI videos using a text-to-video model, processes the output, and uploads the final video to **Google Drive**. This workflow is designed for automated **social media content generation pipelines**.

---

## Features

- Fully automated **AI video generation pipeline**
- Runs on a **scheduled trigger (every 12 hours)**
- Generates **viral short-form video ideas** using AI
- Converts prompts into videos using **text-to-video API**
- Fetches and processes generated video results
- Automatically uploads videos to **Google Drive**
- Structured JSON output for clean automation
- Designed for **YouTube Shorts, TikTok, Instagram Reels** workflows

---

## Workflow Overview

This workflow follows the process below:

1. A **Schedule Trigger** runs every 12 hours
2. A random number is generated to diversify content ideas
3. An AI agent generates:
   - video title
   - description
   - video prompt
4. The prompt is sent to a **text-to-video API**
5. The workflow waits for video generation to complete
6. It fetches the generated video result
7. Parses the response into usable JSON
8. Downloads the generated video file
9. Uploads the final video to **Google Drive**

---

## Nodes Used

### 1. Schedule Trigger
The workflow runs automatically every:

- **12 hours**

This allows continuous automated content generation.

---

### 2. Code in JavaScript
Generates a random number between:

- **1 and 7**

This ensures variation in video idea generation.

---

### 3. Idea Agent (AI Agent)
This node generates structured video content ideas.

It outputs:

- **Title**
- **Description**
- **Prompt**

The AI is instructed to:

- produce viral short-form ideas
- follow strict JSON format
- generate cinematic prompts
- rotate through different video scenarios

---

### 4. OpenRouter Chat Model
The workflow uses:

- `mistralai/mistral-tiny`

This powers the AI idea generation.

---

### 5. Structured Output Parser
Ensures the AI output is always in valid JSON format:

```json
{
  "title": "string",
  "description": "string",
  "prompt": "string"
}
```

This is critical for downstream automation.

---

### 6. HTTP Request (Create Task)
Sends a request to the video generation API:

- Endpoint: `/jobs/createTask`
- Model: `sora-2-text-to-video`

It uses the AI-generated prompt to create a video task.

---

### 7. Wait
Pauses execution while the video is being generated.

This prevents premature fetching of results.

---

### 8. HTTP Request1 (Check Status)
Checks the status of the video generation task using:

- `taskId`

This retrieves the result metadata.

---

### 9. Code in JavaScript1
Parses the API response:

- Converts `resultJson` string into structured JSON
- Extracts video URLs for further processing

---

### 10. HTTP Request2 (Download Video)
Downloads the generated video file from:

- `resultUrls[0]`

---

### 11. Upload File (Google Drive)
Uploads the final video to:

- **Google Drive**
- predefined folder

This completes the automation pipeline.

---

## AI Prompt Structure

The AI generates content in this format:

```json
{
  "title": "Short viral title",
  "description": "Engaging short description",
  "prompt": "Detailed cinematic video prompt"
}
```

---

## Example Workflow Output

- Viral video idea generated
- AI video created using prompt
- Final `.mp4` file downloaded
- Uploaded to Google Drive automatically

---

## Use Cases

This workflow is ideal for:

- automated TikTok content generation
- YouTube Shorts automation
- Instagram Reels automation
- faceless content creation
- viral content testing pipelines
- AI content farms
- marketing automation systems
- creator automation workflows

---

## Requirements

To run this workflow successfully, you need:

- **n8n**
- **OpenRouter API credentials**
- Access to a **text-to-video API (Kie.ai / Sora-like service)**
- **Google Drive OAuth2 credentials**

---

## External Services Used

This workflow integrates with:

- **OpenRouter (LLM)**
- **Kie.ai Video Generation API**
- **Google Drive API**

---

## Setup Instructions

1. Import the JSON workflow into n8n
2. Connect your **OpenRouter credentials**
3. Replace the video API key with your own
4. Update the callback URL if required
5. Connect your **Google Drive account**
6. Set your desired folder for uploads
7. Activate the workflow
8. Wait for scheduled execution or trigger manually
9. Verify that:
   - AI generates valid JSON
   - video task is created
   - result is fetched successfully
   - video uploads to Google Drive

---

## Important Notes

- The workflow is currently **inactive**
- Marked as **Not Tested**, so some adjustments may be required
- Uses:
  - `n_frames: 10`
  - `landscape` aspect ratio
- Callback URL should be replaced with your production endpoint
- API keys are hardcoded and must be secured before deployment

---

## Limitations

- No direct posting to social media platforms yet
- No retry logic for failed video generation
- No validation for API responses
- No content moderation step
- No scheduling logic for posting

---

## Suggested Improvements

You can improve this workflow further by adding:

- direct posting to:
  - TikTok
  - YouTube Shorts
  - Instagram Reels
- caption and hashtag generation
- thumbnail generation
- video storage in cloud buckets
- retry and error handling
- queue-based processing
- multiple video generation per run
- analytics tracking
- content approval step before publishing

---

## Recommended Workflow Expansion

To build a full **AI content engine**, combine this workflow with:

1. Caption generator workflow
2. Hashtag generator
3. Social media posting automation
4. Analytics tracking system

This can evolve into a **fully autonomous content creation SaaS system**.

---

## Example Real-World Flow

Every 12 hours:

1. AI generates a viral idea
2. Converts it into a cinematic prompt
3. Creates a video automatically
4. Downloads the result
5. Uploads it to Google Drive
6. Ready for publishing or automation

This enables **hands-free content production at scale**.

---

## Author

Built as an **n8n AI video generation and content automation workflow** for creators, marketers, and automation builders.

---

## License

You can add your preferred license here, such as:

- MIT
- Apache-2.0
- Proprietary
