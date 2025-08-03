%%
Tags:: #p/project #s/active #t/meta 
%%
# AI Chatbot Gateway - Project Brief

  

## Overview

A stateful AI chatbot library that enables developers to create intelligent chatbots with persistent memory and tool access.

  

## Core Features

  

### 1. Multi-Adapter Architecture

- Currently supports WhatsApp via Baileys adapter

- Designed to support additional chat platforms in the future (Telegram, Discord, Slack, etc.)

  

### 2. System Prompt-Driven Behavior

- All bot behavior, personality, and decision-making is defined through a single system prompt

- No hardcoded logic - the AI interprets the prompt to determine how to respond and when to use tools

  

### 3. Persistent Context Management

- **User Profiles**: Stores user data, preferences, and OAuth tokens

- **Conversation History**: Maintains complete message context for each user

- Both are automatically provided to the AI for context-aware, personalized responses

  

### 4. Extensible Tool System

Current tools:

- **Message Queuing**: Schedule messages to be sent at future times

- **Google OAuth**: Send authentication links for users to connect their Google account

- **Google Calendar**: Create, modify, and check calendar events (requires OAuth)

  

Future tools can be added to extend functionality (e.g., weather, payments, database queries)

  

## Usage Model

Developers use this library to create a single bot instance with:

- A custom system prompt defining the bot's behavior

- Selected tools the bot can access

- Platform adapter configuration

  

The bot then handles all incoming users, maintaining individual context for each while behaving according to its system prompt.