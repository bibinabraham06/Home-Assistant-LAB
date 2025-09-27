# 📦 Detailed Installation Guide

## 🎯 Complete Step-by-Step Installation

This guide will walk you through implementing the complete AI-powered Home Assistant setup from scratch.

## 📋 Pre-Installation Checklist

### ✅ System Requirements Met
- [ ] Home Assistant OS 16.2+
- [ ] Intel NUC or equivalent hardware
- [ ] 8GB+ RAM recommended
- [ ] NVMe SSD storage
- [ ] Stable internet connection

### ✅ API Keys Obtained
- [ ] OpenAI API key from https://platform.openai.com/api-keys
- [ ] Anthropic API key from https://console.anthropic.com/
- [ ] Google AI API key from https://aistudio.google.com/app/apikey

### ✅ Network Configuration
- [ ] Home Assistant accessible at known IP
- [ ] SSH access configured
- [ ] Backup of current configuration created

## 🚀 Installation Process

### Phase 1: Backup Current Configuration

```bash
# SSH into Home Assistant
ssh your-ha-username@your-ha-ip

# Create backup directory
sudo mkdir -p /homeassistant/backups

# Backup current files
sudo cp /homeassistant/configuration.yaml /homeassistant/backups/configuration.yaml.backup
sudo cp /homeassistant/secrets.yaml /homeassistant/backups/secrets.yaml.backup
sudo cp /homeassistant/automations.yaml /homeassistant/backups/automations.yaml.backup
sudo cp /homeassistant/scripts.yaml /homeassistant/backups/scripts.yaml.backup
```

### Phase 2: Deploy Configuration Files

```bash
# Copy new configuration (replace with actual content)
sudo cp configuration.yaml /homeassistant/
sudo cp scripts.yaml /homeassistant/
sudo cp automations.yaml /homeassistant/
```

### Phase 3: Configure API Keys

```bash
# Edit secrets file
sudo nano /homeassistant/secrets.yaml

# Add your actual API keys:
anthropic_api_key: "sk-ant-your-actual-key-here"
openai_api_key: "sk-your-actual-openai-key-here"
google_generative_ai_api_key: "AIza-your-actual-google-key-here"
```

### Phase 4: Install Required Add-ons

1. **Navigate to Add-on Store**:
   - Home Assistant UI → Settings → Add-ons → Add-on Store

2. **Install these add-ons**:
   - **Piper** (Text-to-Speech)
   - **Whisper** (Speech-to-Text)
   - **OpenWakeWord** (Wake word detection)

3. **Configure each add-on**:
   ```yaml
   # Piper configuration
   voice: "en_US-amy-medium"
   speaker: 0

   # Whisper configuration
   model: "base"
   language: "en"

   # OpenWakeWord configuration
   threshold: 0.5
   trigger_level: 1
   ```

### Phase 5: Restart and Validate

```bash
# Restart Home Assistant
# UI: Settings → System → Restart
# Or via SSH: sudo systemctl restart homeassistant
```

### Phase 6: Create Voice Assistants

After restart, create three voice assistants:

#### 1. ChatGPT Creative Assistant
- **Name**: "Creative Assistant"
- **Conversation Agent**: "OpenAI Conversation"
- **Speech-to-Text**: "Faster Whisper"
- **Text-to-Speech**: "Piper"
- **Wake Word**: "OpenWakeWord"
- **Prompt**: "You are a creative AI assistant specialized in storytelling, brainstorming, and imaginative tasks. Be creative and engaging while helping with home automation."

#### 2. Gemini Technical Assistant
- **Name**: "Technical Assistant"
- **Conversation Agent**: "Google Generative AI"
- **Speech-to-Text**: "Faster Whisper"
- **Text-to-Speech**: "Piper"
- **Wake Word**: "OpenWakeWord"
- **Prompt**: "You are a technical AI assistant specializing in analysis, calculations, and technical problem-solving for smart home systems. Be precise and detailed."

#### 3. Claude Home Assistant
- **Name**: "Home Assistant"
- **Conversation Agent**: "Anthropic"
- **Speech-to-Text**: "Faster Whisper"
- **Text-to-Speech**: "Piper"
- **Wake Word**: "OpenWakeWord"
- **Prompt**: "You are the primary smart home AI assistant. Help with device control, automation, and daily home management tasks. Be helpful and efficient."

## 🧪 Testing Installation

### Test 1: AI Integration Check

```yaml
# In Developer Tools → Services
service: conversation.process
data:
  text: "Hello, are you working correctly?"
  agent_id: conversation.anthropic
```

### Test 2: Multi-AI Comparison

```yaml
service: script.ai_model_comparison
data:
  query: "What's the weather like?"
```

### Test 3: Voice Assistant

1. Say wake word: "Hey Assistant"
2. Give command: "Turn on the living room lights"
3. Verify response and action

### Test 4: AI Routing

```yaml
# Should route to Gemini Pro
service: script.smart_ai_selector
data:
  task: "Calculate the energy consumption of my house"

# Should route to ChatGPT
service: script.smart_ai_selector
data:
  task: "Tell me a creative story about smart homes"
```

## 🔧 Configuration Validation

### Check Integration Status

1. **Settings → Devices & Services**
2. Verify these integrations are loaded:
   - ✅ Anthropic
   - ✅ OpenAI Conversation
   - ✅ Google Generative AI

### Check Entity Exposure

1. **Settings → Voice Assistants → Assist**
2. **Exposed Entities tab**
3. Verify only intended entities are exposed

### Check Add-on Status

1. **Settings → Add-ons**
2. Verify all AI add-ons are running:
   - ✅ Piper (Started)
   - ✅ Whisper (Started)
   - ✅ OpenWakeWord (Started)

## ⚠️ Common Installation Issues

### Issue 1: API Integration Failed
**Symptoms**: Integration not loading, error in logs
**Solution**:
1. Verify API key format and validity
2. Check internet connectivity
3. Ensure API key has sufficient credits/quota

### Issue 2: Voice Assistant Not Responding
**Symptoms**: Wake word not detected, no TTS output
**Solution**:
1. Verify add-ons are running
2. Check microphone permissions
3. Test TTS manually in Developer Tools

### Issue 3: High Resource Usage
**Symptoms**: Slow response, high CPU/memory usage
**Solution**:
1. Use lighter Whisper model ("tiny" instead of "base")
2. Reduce AI model token limits
3. Enable more aggressive caching

### Issue 4: Cost Concerns
**Symptoms**: Unexpected API charges
**Solution**:
1. Set spending limits in AI provider dashboards
2. Adjust routing to favor cheaper models
3. Enable more local processing

## 📊 Performance Optimization

### Optimize for Speed
```yaml
# Use faster, smaller models
stt:
  - platform: faster_whisper
    model: "tiny"  # Faster but less accurate

# Reduce token counts
anthropic:
  max_tokens: 500  # Faster responses

# Enable aggressive caching
tts:
  - platform: piper
    cache: true
    cache_dir: "/tmp/tts_cache"
```

### Optimize for Cost
```yaml
# Route more to free/cheap services
ai_task_router:
  default_model: "google_generative_ai"  # Often free
  fallback_model: "anthropic"  # Cost-effective backup
```

### Optimize for Privacy
```yaml
# Maximize local processing
conversation:
  intents:
    simple_commands:
      local_only: true

# Use local models when possible
llm:
  - platform: ollama
    base_url: "http://localhost:11434"
    model: "llama3.2"
```

## 🎯 Post-Installation Steps

### 1. Create Custom Automations
Based on the examples in `automations.yaml`, create automations specific to your home setup.

### 2. Configure Device Groups
Group related devices for easier AI control:
```yaml
light:
  - platform: group
    name: "Living Room Lights"
    entities:
      - light.living_room_main
      - light.living_room_accent
```

### 3. Set Up Monitoring
```yaml
# Monitor AI usage and costs
sensor:
  - platform: rest
    name: "OpenAI Usage"
    resource: "https://api.openai.com/v1/usage"
    headers:
      Authorization: "Bearer !secret openai_api_key"
```

### 4. Document Your Setup
Keep notes on:
- Custom automations created
- Entity exposure changes
- Performance optimizations made
- Usage patterns observed

## 🔄 Maintenance

### Weekly Tasks
- [ ] Check AI integration status
- [ ] Review API usage and costs
- [ ] Test voice assistant functionality
- [ ] Update AI model versions if available

### Monthly Tasks
- [ ] Backup configuration files
- [ ] Review and optimize automations
- [ ] Check for Home Assistant updates
- [ ] Analyze AI usage patterns for optimization

### Quarterly Tasks
- [ ] Review API key security
- [ ] Evaluate new AI models/features
- [ ] Update documentation
- [ ] Consider hardware upgrades if needed

---

**🎉 Installation Complete!**

Your AI-powered Home Assistant system is now ready for advanced automation and intelligent control.

Next: Check out `voice_commands.md` for example commands to try with your new setup.