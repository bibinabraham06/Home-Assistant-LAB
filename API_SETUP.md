# 🔑 API Key Setup Guide

## 🎯 Complete API Configuration Instructions

This guide walks you through obtaining and configuring API keys for all three AI providers in your Home Assistant setup.

## 📋 Required API Keys

You need API keys from these three providers:
1. **Anthropic Claude** (Primary AI)
2. **OpenAI ChatGPT** (Creative AI)
3. **Google Gemini Pro** (Technical AI)

---

## 1. 🤖 Anthropic Claude API Key

### Step 1: Create Anthropic Account
1. Go to: https://console.anthropic.com/
2. Sign up for a new account or log in
3. Verify your email address

### Step 2: Get API Key
1. Navigate to **API Keys** section
2. Click **"Create Key"**
3. Give it a name like "Home Assistant"
4. Copy the key (starts with `sk-ant-`)

### Step 3: Add Credits (If Needed)
- Anthropic requires prepaid credits
- Add at least $20 for testing
- Monitor usage in the console

### Expected Format:
```yaml
anthropic_api_key: "sk-ant-api03-your-actual-key-here"
```

---

## 2. 💬 OpenAI ChatGPT API Key

### Step 1: Create OpenAI Account
1. Go to: https://platform.openai.com/
2. Sign up or log in to your account
3. Complete account verification

### Step 2: Get API Key
1. Go to: https://platform.openai.com/api-keys
2. Click **"Create new secret key"**
3. Name it "Home Assistant AI"
4. Copy the key (starts with `sk-`)

### Step 3: Add Payment Method
1. Go to **Billing** → **Payment methods**
2. Add a credit card for pay-as-you-go
3. Set usage limits if desired

### Expected Format:
```yaml
openai_api_key: "sk-your-actual-openai-key-here"
```

---

## 3. 🧠 Google Gemini Pro API Key

### Step 1: Access Google AI Studio
1. Go to: https://aistudio.google.com/
2. Sign in with your Google account
3. Accept terms of service

### Step 2: Generate API Key
1. Go to: https://aistudio.google.com/app/apikey
2. Click **"Create API Key"**
3. Choose existing project or create new one
4. Copy the key (starts with `AIza`)

### Step 3: Enable Billing (Optional)
- Gemini Pro has a generous free tier
- Billing only needed for high usage
- Monitor usage in Google Cloud Console

### Expected Format:
```yaml
google_generative_ai_api_key: "AIza-your-actual-google-key-here"
```

---

## 🔧 Configure Home Assistant

### Step 1: Edit secrets.yaml
```bash
# SSH into Home Assistant
ssh your-username@your-ha-ip

# Edit secrets file
sudo nano /homeassistant/secrets.yaml
```

### Step 2: Add Your API Keys
Replace the template with your actual keys:
```yaml
# Anthropic Claude API Key
anthropic_api_key: "sk-ant-api03-your-actual-key-here"

# OpenAI ChatGPT API Key
openai_api_key: "sk-your-actual-openai-key-here"

# Google Gemini Pro API Key
google_generative_ai_api_key: "AIza-your-actual-google-key-here"
```

### Step 3: Restart Home Assistant
```bash
# Restart to load new configuration
sudo systemctl restart homeassistant

# Or through UI: Settings → System → Restart
```

---

## 🧪 Test API Integration

### Test 1: Verify All Integrations Load
1. Go to **Settings** → **Devices & Services**
2. Check that these integrations are present:
   - ✅ Anthropic
   - ✅ OpenAI Conversation
   - ✅ Google Generative AI

### Test 2: Test Each AI Provider
```yaml
# Test Claude
service: conversation.process
data:
  text: "Hello Claude, are you working?"
  agent_id: conversation.anthropic

# Test ChatGPT
service: conversation.process
data:
  text: "Hello ChatGPT, are you working?"
  agent_id: conversation.openai

# Test Gemini
service: conversation.process
data:
  text: "Hello Gemini, are you working?"
  agent_id: conversation.google_generative_ai
```

### Test 3: Test AI Routing Script
```yaml
service: script.ai_model_comparison
data:
  query: "What is the optimal temperature for sleeping?"
```

---

## 💰 Cost Management

### Set Spending Limits

#### Anthropic Console
1. Go to **Usage** → **Limits**
2. Set monthly spending limit (e.g., $25)
3. Enable email alerts at 80% usage

#### OpenAI Platform
1. Go to **Usage** → **Limits**
2. Set hard limit (e.g., $30/month)
3. Set soft limit at $25 with email alert

#### Google Cloud Console
1. Go to **Billing** → **Budgets & alerts**
2. Create budget for AI services
3. Set alerts at $10, $15, $20

### Monitor Usage
- Check usage weekly in each provider's console
- Review Home Assistant logs for API call patterns
- Adjust routing rules if costs are high

---

## 🔒 Security Best Practices

### API Key Security
- ✅ Never commit real keys to Git
- ✅ Use secrets.yaml for all keys
- ✅ Rotate keys quarterly
- ✅ Monitor for unauthorized usage

### Access Control
- ✅ Use separate keys for each service
- ✅ Enable IP restrictions if available
- ✅ Monitor API logs for suspicious activity
- ✅ Set up billing alerts for unusual usage

### Backup Strategy
```bash
# Backup your secrets file (encrypted)
sudo cp /homeassistant/secrets.yaml /homeassistant/backups/secrets.yaml.backup

# Ensure backup is secure
sudo chmod 600 /homeassistant/backups/secrets.yaml.backup
```

---

## ⚠️ Troubleshooting API Issues

### Issue: "Invalid API Key" Error
**Causes:**
- Typo in API key
- Key not activated
- Insufficient credits

**Solutions:**
1. Double-check key format and spelling
2. Verify key is active in provider console
3. Add credits/payment method if needed

### Issue: "Rate Limit Exceeded"
**Causes:**
- Too many requests too quickly
- Exceeded monthly quota

**Solutions:**
1. Implement request throttling
2. Increase usage limits
3. Add more credits

### Issue: Integration Not Loading
**Causes:**
- Missing dependencies
- Network connectivity issues
- Configuration errors

**Solutions:**
1. Check Home Assistant logs
2. Restart Home Assistant
3. Verify internet connectivity
4. Check configuration syntax

---

## 📊 Expected Monthly Costs

### Conservative Usage (Testing & Light Use)
- **Claude**: $5-10
- **ChatGPT**: $5-15
- **Gemini**: $0-5 (often free)
- **Total**: $10-30/month

### Moderate Usage (Regular Voice Commands)
- **Claude**: $10-20
- **ChatGPT**: $10-25
- **Gemini**: $5-10
- **Total**: $25-55/month

### Heavy Usage (Frequent AI Interaction)
- **Claude**: $20-40
- **ChatGPT**: $25-50
- **Gemini**: $10-20
- **Total**: $55-110/month

---

**✅ API Setup Complete!**

Once all three API keys are configured and tested, your Home Assistant will have access to the most advanced AI capabilities available in 2025.