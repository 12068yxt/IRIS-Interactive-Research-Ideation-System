# OpenRouter Integration Guide

This guide explains how to configure and use OpenRouter models with the IRIS system.

## Overview

OpenRouter provides access to various LLM models through a unified API interface. This integration allows you to use models like GPT-4, Claude, Llama, and others through OpenRouter's routing capabilities.

## Current Default Configuration

As of the latest update, IRIS now uses **OpenRouter's Google Gemini 2.0 Flash** as the default model for all agents:
- Ideation Agent
- Review Agent  
- Structured Review Agent
- Retrieval components

**Correct Model Identifier**: `openrouter/google/gemini-2.0-flash-001`

## Setup Instructions

### 1. Get OpenRouter API Key

1. Visit [OpenRouter.ai](https://openrouter.ai/) and sign up for an account
2. Navigate to your API keys section
3. Generate a new API key (starts with `sk-or-`)
4. Copy the API key for use in IRIS

### 2. Configure API Key in IRIS

You can configure your OpenRouter API key in two ways:

#### Option A: Through Web Interface (Recommended)
1. Start the IRIS application: `python app.py`
2. Open your browser and navigate to the application
3. Click on the API key management button/modal
4. Select "OpenRouter" from the provider dropdown
5. Enter your OpenRouter API key
6. Click "Save Key"

#### Option B: Environment Variable
Set the environment variable before starting the application:
```bash
export OPENROUTER_API_KEY="sk-or-your-api-key-here"
python app.py
```

### 3. Configure Alternative Models

While the default is now OpenRouter's Gemini 2.0 Flash, you can still use other models by updating your `config/config.yaml` file:

```yaml
ideation_agent:
  model: "openrouter/anthropic/claude-3.5-sonnet"  # Alternative model
  
review_agent:
  model: "openrouter/openai/gpt-4o"  # Alternative model
```

## Important: Model Identifier Format

**Key Point**: When using OpenRouter with LiteLLM, you must use the `openrouter/` prefix followed by the provider/model combination.

**Correct Formats**:
- ✅ `openrouter/google/gemini-2.0-flash-001` (Current default)
- ✅ `openrouter/openai/gpt-4o`
- ✅ `openrouter/anthropic/claude-3.5-sonnet`
- ✅ `openrouter/meta-llama/llama-3.1-405b-instruct`

**Incorrect Formats**:
- ❌ `google/gemini-2.0-flash-001` (Missing openrouter prefix)
- ❌ `gemini/gemini-2.0-flash` (Wrong format entirely)

## Available Models

Some popular OpenRouter models you can use:

- `openrouter/google/gemini-2.0-flash-001` - **Current Default** - Google's latest Gemini model
- `openrouter/openai/gpt-4o` - Latest GPT-4 model
- `openrouter/anthropic/claude-3.5-sonnet` - Claude 3.5 Sonnet
- `openrouter/meta-llama/llama-3.1-405b-instruct` - Llama 3.1 405B
- `openrouter/mistral/mistral-large` - Mistral Large

## Usage Notes

1. **Cost Management**: OpenRouter pricing varies by model. Check their pricing page for current rates.

2. **Rate Limits**: Be aware of OpenRouter's rate limits and quota restrictions.

3. **Fallback Behavior**: The system requires a valid OpenRouter API key to function with OpenRouter models.

4. **Model Performance**: The current default (Gemini 2.0 Flash) offers good balance of performance and cost.

## Troubleshooting

### Common Issues

1. **API Key Not Recognized**
   - Ensure the key starts with `sk-or-`
   - Check that the key is properly formatted
   - Verify the key has not expired

2. **Model Not Available**
   - Confirm you're using the correct format: `openrouter/provider/model-name`
   - Check OpenRouter's model availability
   - Some models may require special access or have waiting lists

3. **Authentication Errors**
   - Verify the API key is correctly set in environment variables or through the web interface
   - Restart the application after setting the API key
   - Ensure the model identifier includes the `openrouter/` prefix

### Debugging Steps

1. Check the application logs for specific error messages
2. Verify API key format matches: `^sk-or-[A-Za-z0-9]{32,}$`
3. Test connectivity to OpenRouter API endpoints
4. Ensure your OpenRouter account has sufficient credits/balance

## Security Considerations

- Never commit API keys to version control
- Use environment variables or the secure web interface for key management
- Regularly rotate your API keys
- Monitor your OpenRouter account for unusual activity

## Support

For issues specific to OpenRouter integration:
- Check OpenRouter's official documentation and status page
- Review IRIS application logs for detailed error information
- Consult the main IRIS README for general troubleshooting