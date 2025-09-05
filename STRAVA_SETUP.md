# Strava API Setup Instructions

## Step 4: Save and Deploy Your Changes

```bash
cd "/Users/zacharyshumaker/Desktop/Working Programs/luke-route-globe"
git add .
git commit -m "Add Strava API credentials for Luke's routes"
git push origin main
```

Wait 2-3 minutes for GitHub Pages to update.

## Step 5: Test With Luke

1. **Send Luke this link**: https://zshumake.github.io/luke-route-globe/

2. **Luke will see**: A "🔗 Connect to Strava" button in the sidebar

3. **Luke clicks the button** and gets redirected to Strava

4. **Luke sees**: "Luke's Route Globe wants to: View data about your activities"

5. **Luke clicks**: "Authorize" (orange button)

6. **Luke gets redirected back** to your app with his routes loaded!

## What Happens Next

- ✅ App loads Luke's 50 most recent activities
- ✅ Fetches GPS coordinates for each route  
- ✅ Displays blue cycling routes, red running routes
- ✅ Shows START/END markers on satellite imagery
- ✅ Luke can click any route to fly to it and see details

## Troubleshooting

**If you see "Invalid client_id":**
- Double-check the Client ID is correct (no quotes, no spaces)

**If Luke gets "Invalid redirect URI":**  
- Make sure Authorization Callback Domain is exactly: `zshumake.github.io`

**If no routes appear after authorization:**
- Check browser console for errors
- Luke might have no GPS-enabled activities (indoor workouts don't have coordinates)

## Security Notes

- ✅ Client Secret is safe in frontend for development/personal use
- ✅ For production apps with many users, move Client Secret to backend
- ✅ Luke can revoke access anytime at strava.com/settings/apps

## API Limits

- 15,000 requests per day per app
- 100 requests per 15 minutes  
- The app includes rate limiting (100ms delays) to stay within limits