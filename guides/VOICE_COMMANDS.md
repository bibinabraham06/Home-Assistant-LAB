# 🎤 Voice Commands & Usage Examples

## 🗣️ Complete Voice Command Reference

This guide provides comprehensive examples of voice commands you can use with your AI-powered Home Assistant setup.

## 🎯 Wake Word Activation

**Primary Wake Word**: "Hey Assistant"
- Say the wake word clearly
- Wait for confirmation tone
- Speak your command within 10 seconds

---

## 🤖 AI Provider Routing

Your system automatically routes commands to the best AI:

### 🎨 Creative Tasks → ChatGPT
Commands containing: *creative, story, poem, joke, brainstorm, imagine, write*

### 🔧 Technical Tasks → Gemini Pro
Commands containing: *analyze, calculate, technical, code, debug, compute, measure*

### 🏠 Home Control → Claude (Default)
All other commands including: *control, automation, status, help*

---

## 🏠 Home Control Commands

### Lighting Control
- *"Turn on the living room lights"*
- *"Dim the bedroom lights to 50%"*
- *"Set all lights to warm white"*
- *"Turn off all lights except the hallway"*
- *"Create romantic lighting in the dining room"*

### Climate Control
- *"Set the temperature to 72 degrees"*
- *"Turn on the air conditioning"*
- *"What's the current temperature?"*
- *"Make it warmer in the bedroom"*
- *"Turn off the heat"*

### Device Control
- *"Turn on the TV"*
- *"Start the robot vacuum"*
- *"Lock all doors"*
- *"Turn on the coffee maker"*
- *"Open the garage door"*

### Scene Activation
- *"Activate movie night scene"*
- *"Set good morning routine"*
- *"Turn on bedtime mode"*
- *"Activate away mode"*
- *"Set romantic dinner lighting"*

### Status Inquiries
- *"What's the status of all sensors?"*
- *"Are all doors locked?"*
- *"What lights are currently on?"*
- *"Is the security system armed?"*
- *"What's the current energy usage?"*

---

## 🎨 Creative Commands (ChatGPT)

### Storytelling
- *"Tell me a bedtime story about smart lights"*
- *"Create a funny story about my robot vacuum"*
- *"Imagine what my house would say if it could talk"*
- *"Write a poem about home automation"*

### Entertainment
- *"Tell me a joke about smart homes"*
- *"Create a riddle about my devices"*
- *"Suggest a creative name for my robot vacuum"*
- *"Write a song about my morning routine"*

### Planning & Ideas
- *"Brainstorm automation ideas for my home"*
- *"Create a creative lighting plan for dinner parties"*
- *"Suggest unique ways to use my smart speakers"*
- *"Imagine future home automation possibilities"*

### Writing Assistance
- *"Help me write a description of my smart home"*
- *"Create a creative shopping list"*
- *"Write a funny review of my smart thermostat"*
- *"Compose a letter to my future smart home"*

---

## 🔧 Technical Commands (Gemini Pro)

### Analysis & Calculations
- *"Analyze my energy consumption patterns"*
- *"Calculate the cost savings from LED bulbs"*
- *"Compute optimal thermostat settings"*
- *"Analyze which devices use the most power"*

### Troubleshooting
- *"Debug why my automation isn't working"*
- *"Analyze network connectivity issues"*
- *"Technical analysis of my smart home performance"*
- *"Calculate optimal placement for sensors"*

### Data & Metrics
- *"Measure the efficiency of my current setup"*
- *"Calculate monthly energy costs"*
- *"Analyze temperature patterns over the last week"*
- *"Compute the ROI of my smart home investment"*

### Technical Planning
- *"Technical requirements for adding new devices"*
- *"Analyze bandwidth usage of my smart devices"*
- *"Calculate wireless signal strength needed"*
- *"Technical specs for upgrading my network"*

---

## 💬 Conversation Commands (Claude)

### Information Requests
- *"What's the weather forecast?"*
- *"What time is it?"*
- *"What's on my calendar today?"*
- *"Tell me about today's news"*

### Home Management
- *"Create a maintenance schedule for my devices"*
- *"Help me organize my automations"*
- *"Suggest improvements for my smart home"*
- *"Plan my energy usage for this week"*

### Learning & Guidance
- *"Explain how my smart thermostat works"*
- *"Teach me about home automation best practices"*
- *"Help me understand my energy bill"*
- *"What are the benefits of smart lighting?"*

### Personal Assistant
- *"Remind me to check the air filter"*
- *"Add milk to my shopping list"*
- *"Set a timer for 20 minutes"*
- *"What should I make for dinner?"*

---

## 🧪 Testing & Comparison Commands

### AI Model Comparison
- *"Compare responses: What's the best temperature for sleeping?"*
- *"Test all models: How can I save energy at home?"*
- *"Multi-AI query: What's the future of smart homes?"*

### System Testing
- *"Test voice recognition quality"*
- *"Check all AI integrations status"*
- *"Verify text-to-speech is working"*
- *"Test wake word detection"*

---

## 🎛️ Advanced Automation Commands

### Conditional Logic
- *"If it's raining, turn on the porch lights"*
- *"When I leave, activate security mode"*
- *"If energy usage is high, dim non-essential lights"*
- *"When bedtime, lock doors and arm security"*

### Multi-Device Coordination
- *"Coordinate all lights for movie night"*
- *"Sync music throughout the house"*
- *"Create a whole-house wake-up sequence"*
- *"Orchestrate a security response"*

### Learning Commands
- *"Learn my lighting preferences"*
- *"Adapt to my daily routine"*
- *"Optimize based on my usage patterns"*
- *"Suggest automations based on my habits"*

---

## 🔊 Voice Response Settings

### Customizing TTS Responses

#### Detailed Responses
- *"Give me detailed status of all devices"*
- *"Explain what you just did"*
- *"Provide full automation details"*

#### Brief Responses
- *"Just confirm completion"*
- *"Brief status only"*
- *"Quick acknowledgment please"*

#### Silent Mode
- *"Execute without voice response"*
- *"Silent mode for this command"*
- *"Visual feedback only"*

---

## 🎯 Context-Aware Commands

### Time-Based Context
- *"Good morning" (activates morning routine)*
- *"Good night" (activates bedtime routine)*
- *"I'm home" (deactivates away mode)*
- *"Leaving now" (activates away mode)*

### Location-Based Context
- *"Living room lights" (current room context)*
- *"Upstairs temperature" (floor-specific)*
- *"Kitchen devices" (room-specific)*
- *"Outdoor lights" (area-specific)*

### Activity-Based Context
- *"Cooking mode" (kitchen-focused)*
- *"Work mode" (office-focused)*
- *"Entertainment mode" (media-focused)*
- *"Cleaning mode" (maintenance-focused)*

---

## ⚠️ Voice Command Troubleshooting

### If Commands Aren't Recognized
1. **Speak clearly** and at normal pace
2. **Reduce background noise**
3. **Use exact device names** from your HA config
4. **Check wake word detection** is active
5. **Verify microphone permissions**

### If Wrong AI Responds
- **Add specific keywords** for routing
- **Use explicit AI names**: "Ask ChatGPT to..."
- **Check routing rules** in scripts.yaml
- **Adjust keyword patterns** if needed

### If TTS Isn't Working
1. **Check Piper add-on** is running
2. **Verify speaker output** is configured
3. **Test TTS manually** in Developer Tools
4. **Check volume levels** on device

---

**🎤 Voice Control Ready!**

Your AI-powered Home Assistant now responds to natural language commands with intelligent routing to the best AI for each task.