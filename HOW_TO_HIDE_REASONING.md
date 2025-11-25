# How to Hide Reasoning Thoughts and References

## 🎯 **The Real Solution**

The ChatKit API doesn't have parameters to hide reasoning thoughts and transcript references. These are controlled by **your OpenAI workflow configuration** in the Agent Builder.

## 🔧 **How to Actually Hide These Elements**

### **Method 1: Configure Your Workflow (Recommended)**

1. **Go to OpenAI Agent Builder**: https://platform.openai.com/agent-builder
2. **Open your workflow**: `wf_68f1027d2f8c8190abecaadf0620ceda0de6e9b9f2a6dbae`
3. **In the workflow settings**, look for:
   - **"Show reasoning"** - Set to `false`
   - **"Show references"** - Set to `false`
   - **"Show tool calls"** - Set to `false`
4. **Save and republish** the workflow
5. **The ChatKit interface will automatically respect** these settings

### **Method 2: Modify Your Agent Prompt**

In your workflow, add instructions to the agent prompt:

```
You are a sales agent. When responding:
- Do not show your reasoning process
- Do not show source references or citations
- Provide clean, direct responses only
- Focus on helping the customer
```

### **Method 3: Use Response Formatting**

Configure your workflow to use structured output that doesn't include reasoning:

```json
{
  "response": "Your clean response here",
  "no_reasoning": true,
  "no_references": true
}
```

## ✅ **Current Status**

Your ChatKit app is now working correctly with:

- ✅ **File uploads enabled**
- ✅ **Clean session creation**
- ✅ **No API errors**
- ✅ **Proper workflow connection**

## 🌐 **Test Your App**

1. **Open**: http://localhost:3000
2. **Wait for session to load**
3. **Ask a question** to test the workflow
4. **Check if reasoning/references are hidden** in the response

## 🔄 **If You Still See Reasoning/References**

The issue is in your **OpenAI workflow configuration**, not the ChatKit app. You need to:

1. **Edit your workflow** in Agent Builder
2. **Configure the output format** to hide internal details
3. **Republish the workflow**
4. **Test again** in the ChatKit interface

The ChatKit interface will automatically display whatever your workflow outputs, so the control is in the workflow settings, not the ChatKit configuration.
