FROM ubuntu:24.04
ENV DEBIAN_FRONTEND=noninteractive

# Install essentials and Claude Code (without post-install scripts)
RUN apt-get update && apt-get install -y \
    curl git sudo ca-certificates 
    
# Install Node.js 18.x (LTS) from NodeSource
RUN curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash - \
    && apt-get install -y nodejs


RUN npm install -g @openai/codex
RUN npm install -g @github/copilot
RUN npm install -g @anthropic-ai/claude-code
RUN npm install -g cline
RUN npm install -g opencode-ai

COPY opencode.json /root/.config/opencode/opencode.json


