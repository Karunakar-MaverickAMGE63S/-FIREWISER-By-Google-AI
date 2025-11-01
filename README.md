<div align="center">
<img width="1200" height="475" alt="GHBanner" src="https://github.com/user-attachments/assets/0aa67016-6eaf-458a-adb2-6e31a0763ed6" />
</div>

# Run and deploy your AI Studio app

This contains everything you need to run your app locally.

https://firewiser-416455034441.us-west1.run.app

## Run Locally

**Prerequisites:**  Node.js


1. Install dependencies:
   `npm install`
2. Set the `GEMINI_API_KEY` in [.env.local](.env.local) to your Gemini API key
3. Run the app:
   `npm run dev`
Based on the structure and components of the React application (e.g., `App.tsx`, `aiService.ts`, and the defined `Step` and `Role` enums), here are the testing instructions to verify the key features of the application, particularly the AI-driven guidance and map visualization.

-----

## 🧪 Application Testing Instructions (FIREWISER)

This application is designed to provide personalized emergency guidance (using Gemini) and operational data (Google Maps/Air Quality API) based on a user's location and role.

### **Pre-requisite Setup**

Before testing, ensure your API keys are correctly configured to prevent fallback data usage:

1.  **Check Gemini Key:** In **`.env.local`**, ensure `GEMINI_API_KEY` is set to a valid key, not `PLACEHOLDER_API_KEY`.
2.  **Run Application:** Start your local development server using the command specified in your `README.md` and `package.json`:
    ```bash
    npm install
    npm run dev
    ```
    The application should open in your browser, typically at `http://localhost:3000`.

-----

### **Test Scenario 1: Personalized Evacuation Guidance (Gemini Integration)**

This test verifies the main feature: generating personalized, AI-driven emergency guidance. This relies on the Gemini API key.

| Step | Action | Expected Result | Pass/Fail |
| :--- | :--- | :--- | :--- |
| **1. Input** | On the initial screen (Step 1), enter a **ZIP Code** (e.g., `90265`) and select a **Role** (e.g., `Parents with Young Children`). Click **"Get Wise Guidance"**. | The app proceeds to the **Consent** screen (Step 2). | |
| **2. Consent** | Click **"I Agree to AI Generation"** (The prompt for the AI is now sent). | The app transitions to the **Loading** screen (Step 3). The network tab in your browser console should show a successful API call to the Gemini endpoint. | |
| **3. Guidance View** | After a brief loading time, the **Wise Output** screen (Step 4) is displayed. | The page shows three distinct sections with emergency information: <br> **a. Alert:** A bold, urgent evacuation message. <br> **b. Checklist:** A title and a list of specific, role-based steps (e.g., "Secure Children First"). <br> **c. Coach:** A short, encouraging message. | |
| **4. Role Variation** | Click the **"Checklist"** button to view the full checklist (Step 4a). Then, start over (back to Step 1). Repeat Steps 1-3, but select a different role (e.g., `Adults-Only Household`). | The generated **Alert**, **Checklist Items**, and **Coach Message** should be meaningfully different and tailored to the new selected role. | |

### **Test Scenario 2: Dynamic Triage and Map Overlay (Maps/Air Quality Integration)**

This test verifies the map and external data integration for emergency responders (Command View). This relies on the Google Maps and Air Quality API keys.

| Step | Action | Expected Result | Pass/Fail |
| :--- | :--- | :--- | :--- |
| **5. Command Input** | From the main input screen (Step 1), click the **"Command"** button. | The app proceeds to the **Command Loading** screen (Step\_CommandLoading). | |
| **6. Command View** | The app transitions to the **Command View** (Step 5). | A map is displayed. It should feature a colored border (defined by a wind direction/hazard color) and an overlay of small moving "dots" representing assets (as configured in `constants.tsx`). | |
| **7. Air Operations** | On the Command View, click the **"Air Quality Operations"** button. | The app transitions to the **Air Ops Loading** screen (Step 5a), and then to the **Air Ops View** (Step 6). | |
| **8. Air Ops Data** | On the Air Ops View (Step 6), observe the left-hand panel. | This panel should display the following data, fetched via the Air Quality API: <br> **a. AQI Value:** A number (Air Quality Index). <br> **b. AQI Category:** Text description (e.g., "Good," "Moderate"). <br> **c. Dominant Pollutant.** | |

### **Test Scenario 3: Chrome Built-in AI Functionality (Client-Side AI)**

This test is conditional and requires a compatible version of the Chrome browser with the experimental Built-in AI feature enabled. This functionality is implemented in `chromeAiService.ts`.

| Step | Action | Expected Result | Pass/Fail |
| :--- | :--- | :--- | :--- |
| **9. Browser Check** | Open the browser console (F12) and type `window.ai.canCreateSummarizer()`. | If the feature is available, the result will be a Promise that resolves to `'readily'`. If not, it will be `'no'`. **(Test is only valid if result is 'readily')** | |
| **10. AI Service Call** | Use the application's built-in Chrome AI features (if accessible). *Since there is no visible UI button for this feature in `App.tsx`, you would need to manually call a function from the console.* | Calling a function like `rewriteText("This is an old message.")` from your component or the console (if exposed globally) should return a rephrased version of the text without making a network API call. | |
