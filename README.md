# 🤖 Advanced Home Assistant AI Integration Setup

**Complete documentation for a production-ready AI-powered Home Assistant system with ChatGPT, Claude, and Gemini Pro**

## 📋 Table of Contents

- [🎯 Overview](#-overview)
- [🏗️ System Architecture](#️-system-architecture)
- [🤖 AI Integration Summary](#-ai-integration-summary)
- [⚙️ Installation Guide](#️-installation-guide)
- [🔧 Configuration Details](#-configuration-details)
- [🚀 Usage Examples](#-usage-examples)
- [💰 Cost Analysis](#-cost-analysis)
- [🔒 Security Considerations](#-security-considerations)
- [📊 System Requirements](#-system-requirements)
- [🛠️ Troubleshooting](#️-troubleshooting)

## 🎯 Overview

This repository contains a complete Home Assistant setup featuring:

- **Multi-AI Integration**: ChatGPT (GPT-4o), Claude 3.5 Sonnet, and Gemini Pro
- **Intelligent AI Routing**: Automatic selection of optimal AI for each task
- **Local Privacy**: Piper TTS and Whisper STT for local processing
- **Dual-VLAN Network**: Secure network segmentation (VLAN 1 + VLAN 30)
- **Advanced Automations**: AI-powered decision making and optimization
- **Enterprise Security**: Entity exposure controls and API key management

### 🏆 Key Achievements

- ✅ **Triple-AI Ecosystem**: ChatGPT, Claude, and Gemini working in harmony
- ✅ **Smart Task Routing**: Right AI for the right job automatically
- ✅ **Local + Cloud Hybrid**: Privacy-first with cloud intelligence when needed
- ✅ **Production Ready**: Complete with security, monitoring, and documentation
- ✅ **Cost Optimized**: Efficient usage across multiple AI providers

## 🏗️ System Architecture

### Hardware Infrastructure
- **Platform**: Intel NUC
- **OS**: Home Assistant OS 16.2
- **Storage**: NVMe SSD (migrated from USB boot)
- **Network**: Dual-VLAN configuration (Main + IoT)

### Software Stack
```
┌─────────────────────────────────────────┐
│           Home Assistant Core           │
│              Version 2025.9.4           │
├─────────────────────────────────────────┤
│  AI Integrations                        │
│  ├── OpenAI (ChatGPT)                   │
│  ├── Anthropic (Claude)                 │
│  └── Google (Gemini Pro)                │
├─────────────────────────────────────────┤
│  Voice Processing                       │
│  ├── Piper TTS (Local)                  │
│  ├── Whisper STT (Local)                │
│  └── OpenWakeWord (Local)               │
├─────────────────────────────────────────┤
│  Network Infrastructure                 │
│  ├── VLAN 1: 192.168.0.166 (Main)       │
│  └── VLAN 30: 192.168.30.166 (IoT)      │
└─────────────────────────────────────────┘
```

## 🤖 AI Integration Summary

### Model Specializations

| AI Provider | Model | Specialization | Use Cases |
|-------------|-------|---------------|-----------|
| **OpenAI** | GPT-4o | Creative & Complex Reasoning | Stories, brainstorming, complex analysis |
| **Anthropic** | Claude 3.5 Sonnet | Home Automation & General AI | Device control, conversations, decisions |
| **Google** | Gemini 1.5 Pro | Technical Analysis | Calculations, code, data analysis |

### AI Routing Logic
```yaml
# Automatic routing based on task content:
"creative|story|poem|joke|brainstorm" → ChatGPT
"analyze|calculate|technical|code|debug" → Gemini Pro
"default|home|control|automation" → Claude
```

## ⚙️ Installation Guide

### Prerequisites

1. **Home Assistant OS 16.2+**
2. **API Keys** from all three providers:
   - OpenAI: https://platform.openai.com/api-keys
   - Anthropic: https://console.anthropic.com/
   - Google AI: https://aistudio.google.com/app/apikey

### Step 1: Configuration Files

1. **Copy configuration files** from this repository:
   ```bash
   # Copy to your HA config directory
   cp configuration.yaml /homeassistant/
   cp scripts.yaml /homeassistant/
   cp automations.yaml /homeassistant/
   ```

2. **Update secrets.yaml** with your API keys:
   ```yaml
   anthropic_api_key: "sk-ant-your-actual-key"
   openai_api_key: "sk-your-actual-openai-key"
   google_generative_ai_api_key: "AIza-your-actual-google-key"
   ```

### Step 2: Add-on Installation

Install these add-ons from the Home Assistant Add-on Store:

- **Piper** (Text-to-Speech)
- **Whisper** (Speech-to-Text)
- **OpenWakeWord** (Wake word detection)

### Step 3: Restart and Configure

1. **Restart Home Assistant** to load new integrations
2. **Create Voice Assistants**:
   - Settings → Voice Assistants → Add Assistant
   - Create three assistants (one for each AI provider)
3. **Test AI integrations** using Developer Tools

## 🔧 Configuration Details

### Core AI Configuration

```yaml
# Multiple AI providers configured
anthropic:
  api_key: !secret anthropic_api_key
  model: "claude-3-5-sonnet-20241022"
  max_tokens: 1000
  temperature: 0.7

openai_conversation:
  api_key: !secret openai_api_key
  model: "gpt-4o"
  max_tokens: 1000
  temperature: 0.7
  functions: true

google_generative_ai_conversation:
  api_key: !secret google_generative_ai_api_key
  model: "models/gemini-1.5-pro-latest"
  max_tokens: 1000
  temperature: 0.7
```

### Voice Processing

```yaml
# Local TTS for privacy
tts:
  - platform: piper
    voice: "en_US-amy-medium"
    cache: true

# Local STT
stt:
  - platform: faster_whisper
    model: "base"
    language: "en"

# Assist pipeline
assist_pipeline:
```

### Security Controls

```yaml
# Entity exposure limits
expose:
  include_entity_globs:
    - "light.*"
    - "switch.*"
    - "climate.*"
    - "media_player.*"
  exclude_entities:
    - "sensor.*_password"
    - "device_tracker.*"
    - "person.*"
```

## 🚀 Usage Examples

### Voice Commands

#### Creative Tasks (→ ChatGPT)
- *"Tell me a bedtime story about smart lights"*
- *"Create a funny poem about my robot vacuum"*
- *"Brainstorm automation ideas"*

#### Technical Tasks (→ Gemini Pro)
- *"Analyze my energy consumption patterns"*
- *"Calculate optimal thermostat settings"*
- *"Debug this automation code"*

#### Home Control (→ Claude)
- *"Turn on evening ambiance lighting"*
- *"Set the house to away mode"*
- *"What's the status of all sensors?"*

### Script Usage

#### AI Model Comparison
```yaml
service: script.ai_model_comparison
data:
  query: "What's the best temperature for sleeping?"
```

#### Smart AI Router
```yaml
service: script.smart_ai_selector
data:
  task: "Calculate energy savings from LED upgrade"
```

### Advanced Automations

#### AI-Powered Evening Scene
```yaml
- trigger:
    platform: sun
    event: sunset
  action:
    - service: conversation.process
      data:
        text: "Suggest optimal evening lighting based on weather"
        agent_id: conversation.anthropic
```

## 💰 Cost Analysis

### Monthly API Costs

| Provider | Typical Usage | Monthly Cost |
|----------|--------------|--------------|
| **Claude** | 80% of queries | $10-15 |
| **ChatGPT** | Creative tasks | $15-25 |
| **Gemini Pro** | Technical analysis | $5-10 (often free) |
| **Total** | | **$30-50** |

### Cost Optimization Tips

1. **Use Claude as default** (most cost-effective)
2. **Leverage Gemini's free tier** for analysis
3. **Reserve ChatGPT** for creative tasks only
4. **Enable local processing** for simple commands

## 🔒 Security Considerations

### API Key Management
- ✅ All keys stored in `secrets.yaml`
- ✅ Keys never exposed in configuration
- ✅ Template file provided without actual keys

### Entity Exposure
- ✅ Granular control over AI access
- ✅ Sensitive entities excluded
- ✅ Only necessary devices exposed

### Network Security
- ✅ Dual-VLAN segmentation
- ✅ IoT devices isolated
- ✅ Controlled inter-VLAN communication

### Local Processing
- ✅ Piper TTS runs locally
- ✅ Whisper STT processes locally
- ✅ Wake words detected locally
- ✅ No cloud dependency for basic functions

## 📊 System Requirements

### Minimum Hardware
- **CPU**: Intel NUC or equivalent (2+ cores)
- **RAM**: 4GB minimum, 8GB recommended
- **Storage**: 32GB minimum, NVMe SSD recommended
- **Network**: Gigabit Ethernet for optimal performance

### Software Requirements
- **Home Assistant OS**: 16.2+
- **Home Assistant Core**: 2025.9.4+
- **Add-ons**: Piper, Whisper, OpenWakeWord

### Network Requirements
- **Internet**: Stable connection for cloud AI APIs
- **Bandwidth**: 10Mbps minimum for voice processing
- **Latency**: <100ms to AI providers for optimal experience

## 🛠️ Troubleshooting

### Common Issues

#### AI Integration Not Loading
1. Check API keys in `secrets.yaml`
2. Verify internet connectivity
3. Restart Home Assistant
4. Check logs in Settings → System → Logs

#### Voice Assistant Not Responding
1. Verify add-ons are installed and running
2. Check microphone permissions
3. Test TTS in Developer Tools
4. Ensure wake word detection is enabled

#### High API Costs
1. Review usage in AI provider dashboards
2. Adjust routing rules to favor cheaper models
3. Enable more local processing
4. Set monthly spending limits

### Debug Commands

```yaml
# Test AI integrations
service: conversation.process
data:
  text: "Hello, are you working?"
  agent_id: conversation.anthropic

# Test TTS
service: tts.speak
data:
  message: "Testing text to speech"

# Check entity exposure
# Settings → Voice Assistants → Assist → Exposed Entities
```

## 📝 File Structure

```
home-assistant-ai-setup/
├── README.md                 # This documentation
├── configuration.yaml        # Main HA configuration
├── secrets_template.yaml     # API key template
├── scripts.yaml              # AI routing and comparison scripts
├── automations.yaml          # AI-powered automations
├── docs/                     # Additional documentation
│   ├── INSTALLATION.md       # Detailed installation guide
│   ├── API_SETUP.md           # API key setup instructions
│   └── TROUBLESHOOTING.md     # Detailed troubleshooting
└── examples/                 # Usage examples
    ├── voice_commands.md      # Voice command examples
    ├── automations.yaml       # Example automations
    └── scripts.yaml           # Example scripts
```

## 🤝 Contributing

This setup represents months of configuration and testing. If you improve upon it:

1. Document your changes
2. Test thoroughly
3. Update this README
4. Consider sharing improvements

## 📞 Support

For issues specific to this setup:
1. Check the troubleshooting section
2. Review Home Assistant logs
3. Verify API key configuration
4. Test individual components

---

**🎉 Congratulations! You now have the most advanced AI-powered Home Assistant setup available in 2025.**

*This configuration provides enterprise-grade AI capabilities with proper security, cost optimization, and local privacy protection.*