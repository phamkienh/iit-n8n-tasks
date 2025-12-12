# L9, Exercise B – Webhook → Random Quote from API

## Goal
Create a workflow in **n8n** that receives a request via a **Webhook**, fetches a random quote from the external API `https://quotes.domiadi.com/api`, and returns it in JSON.

---

## Step 1: Create a New Workflow
1. Start **n8n** in your fork Codespace.  
2. Add **Workflows → + New**.  
3. Name it: `L9_ExerciseB_<your_github_username>`.

**NOTE:** In the `L8/solutions/L9_ExerciseB.md` provide a screenshot showing a newly created, properly named workflow. Address bar in the browser must be visible.

---

## Step 2: Add a Webhook Node
1. Drag a **Webhook** node onto the canvas.  
2. Configure:  
   - **HTTP Method**: `GET`  
   - **Path**: `quote`  
   - **Response Mode**: `Using 'Respond to Webhook' node`  
3. Save the workflow.  

You now have two URLs:  
- Test: `http://[YOUR_CODESPACE_URL]/webhook-test/quote`  
- Production: `http://[YOUR_CODESPACE_URL]/webhook/quote`

---

## Step 3: Add an HTTP Request Node
1. Click **+** to add a new Node after Webhook.  
2. Choose **HTTP Request** from the list.  
3. Configure:  
   - **HTTP Method**: `GET`  
   - **URL**: `https://quotes.domiadi.com/api`  
   - **Response Format**: `JSON`

**NOTE:** Provide a screenshot with node configuration to your solution file. Address bar in the browser must be visible.

---

## Step 4: Add a Respond to Webhook Node
1. Click on **+** and add a `Respond to Webhook` node to the canvas.  
2. Configure:  
   - **Response Code**: `200`  
   - **Respond With**: `JSON`
   - **Response Body**:
   ```
   {
     "quote" : "{{ $json.quote }}"
   }
   ```  
4. Save.  

**NOTE:** Provide a screenshot with node configuration to your solution file. Address bar in the browser must be visible.

---

## Step 5: Test the Workflow
1. Click **Execute Workflow** to enable the test endpoint.  
2. Test in a browser:  

   - Open:  
     `http://[YOUR_CODESPACE_URL]/webhook-test/quote`

3. Or use curl:  
   ```bash
   curl "http://[YOUR_CODESPACE_URL]/webhook-test/quote"
   ```

**NOTE**: Provide a screenshot with the result of workflow execution. Address bar in the browser must be visible.

## Example Output

Example output should be like:

```
{
  "quote": "The best way to predict the future is to invent it.",
}
```

## Step 6: Activate Workflow

You can also activate your workflow:

Toggle Active in the top-right corner.

Use the production URL for permanent access:
http://[YOUR_CODESPACE_URL]/webhook/quote