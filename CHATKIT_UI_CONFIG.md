# ChatKit UI Configuration Guide

## 🎯 **ChatKit Configuration**

This guide shows the available configuration options for the ChatKit interface. Note that reasoning thoughts and transcript references are controlled by the workflow itself, not by ChatKit configuration parameters.

## 📋 **Configuration Options**

### **Current Settings (in `lib/config.ts`)**

```typescript
export const CHATKIT_CONFIG = {
  file_upload_enabled: true, // Enable file uploads
};
```

### **What Each Option Controls**

| Option                | Description                       | Default | Effect                  |
| --------------------- | --------------------------------- | ------- | ----------------------- |
| `file_upload_enabled` | Enables file upload functionality | `true`  | Allows document uploads |

### **Important Note About Reasoning & References**

**Reasoning thoughts and transcript references are controlled by your OpenAI workflow configuration, not by ChatKit parameters.** To hide these elements:

1. **Configure your workflow** in the OpenAI Agent Builder
2. **Set the workflow to not show reasoning** in the workflow settings
3. **The ChatKit interface will automatically respect** the workflow's output format

## 🔧 **How to Change Settings**

### **Option 1: Edit the Config File**

1. Open `lib/config.ts`
2. Modify the `CHATKIT_CONFIG` object
3. Restart the development server

### **Option 2: Environment Variables**

You can also make these configurable via environment variables by updating the config:

```typescript
export const CHATKIT_CONFIG = {
  show_reasoning: process.env.NEXT_PUBLIC_SHOW_REASONING === "true",
  show_references: process.env.NEXT_PUBLIC_SHOW_REFERENCES === "true",
  show_tool_calls: process.env.NEXT_PUBLIC_SHOW_TOOL_CALLS === "true",
  file_upload_enabled: process.env.NEXT_PUBLIC_FILE_UPLOAD_ENABLED !== "false",
};
```

Then add to your `.env.local`:

```bash
NEXT_PUBLIC_SHOW_REASONING=false
NEXT_PUBLIC_SHOW_REFERENCES=false
NEXT_PUBLIC_SHOW_TOOL_CALLS=false
NEXT_PUBLIC_FILE_UPLOAD_ENABLED=true
```

## 🎨 **UI Behavior**

### **With Current Settings (All Hidden)**

- ✅ Clean, simple chat interface
- ✅ Only shows final responses
- ✅ No internal reasoning visible
- ✅ No source references shown
- ✅ No tool call details displayed

### **If You Want to Show Everything**

```typescript
export const CHATKIT_CONFIG = {
  show_reasoning: true, // Show reasoning thoughts
  show_references: true, // Show transcript references
  show_tool_calls: true, // Show tool call details
  file_upload_enabled: true, // Enable file uploads
};
```

## 🚀 **Testing the Configuration**

1. **Start the app**: `npm run dev`
2. **Open**: http://localhost:3000
3. **Test with a question** that would normally show reasoning/references
4. **Verify** that only the clean response is shown

## 📝 **Example Scenarios**

### **For Sales Agent (Recommended)**

```typescript
// Clean, professional interface
show_reasoning: false,      // Hide internal thoughts
show_references: false,     // Hide transcript sources
show_tool_calls: false,     // Hide RAG calls
```

### **For Development/Debugging**

```typescript
// Full visibility for debugging
show_reasoning: true,       // See how AI thinks
show_references: true,      // See which transcripts used
show_tool_calls: true,      // See RAG function calls
```

### **For Mixed Use**

```typescript
// Show sources but hide reasoning
show_reasoning: false,      // Clean responses
show_references: true,      // Show transcript sources
show_tool_calls: false,     // Hide technical details
```

## 🔄 **Restart Required**

After changing these settings, you need to restart the development server:

```bash
# Stop the server (Ctrl+C)
# Then restart
npm run dev
```

The configuration is applied when the ChatKit session is created, so changes require a fresh session.
