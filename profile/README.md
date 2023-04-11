# Chat-GPT Assistant
It's a clone (MVP) of the ChatGPT.

Basic funtionality is implemented:
- Create, Delete, Delete all, Update title for Chats
- Post messages to a chat and generate GPT response
- Stop and Regenerate GPT responses
- Edit User messages and switch between threads
- Voice input powered by Whisper API and voice output built with Browser API

What is not implemented:
- Pagination for chats and messages on UI
- Rendering performance for the conversation can be improved
- Some bugs are not fixed

Feel free to submit PRs and make forks.

## Demo
[![Demo](https://img.youtube.com/vi/3ZJGMk3eBqk/0.jpg)](https://youtu.be/3ZJGMk3eBqk)

## How to Run

### Create OpenAI API Account

1. Sign up for an OpenAI API account at [https://platform.openai.com/signup](https://platform.openai.com/signup).
2. Generate an [API Key](https://platform.openai.com/account/api-keys).

### Prerequisites

- Install Git: Follow the instructions on the [official Git documentation](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) to install Git.
- Install Docker: Install Docker by following the instructions on the [official Docker documentation](https://docs.docker.com/get-docker/).

### Backend Setup

1. Clone the backend repository:

   ```bash
   git clone https://github.com/chat-gpt-assistant/assistant-back.git
   cd assistant-back
   ```
   
2. Update the `src/main/resources/application-docker.yml` file with your OpenAI API key

3. Run MongoDB using the `mongo.yml` from the project:

   ```bash
   docker-compose -f ./src/main/docker/mongo.yml up -d
   ```

4. Build the Docker image of the backend using Jib:

   ```bash
   ./gradlew jibDockerBuild
   ```

5. Run the backend Docker image with network for MongoDB and opened ports for the REST API:

   ```bash
   docker run -d -p 8080:8080 --network docker_chatgptassistant-net -e SPRING_PROFILES_ACTIVE=docker --name chat-gpt-assistant com.github.chat-gpt-assistant/assistant-back:0.0.1-SNAPSHOT
   ```

### UI Setup

1. Clone the UI repository:

   ```bash
   git clone https://github.com/chat-gpt-assistant/assistant-ui.git
   cd assistant-ui
   ```

2. Build the UI Docker image:

   ```bash
   docker build -t assistant-ui -f ./docker/Dockerfile .
   ```

3. Run the UI Docker image:

   ```bash
   docker run -d -p 3000:80 --name assistant-ui assistant-ui
   ```

The front-end UI will now be available at [http://localhost:3000](http://localhost:3000).
