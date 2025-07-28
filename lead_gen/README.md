# Google Maps Business Email Scraper

A powerful n8n workflow that extracts business emails from Google Maps listings without requiring any paid APIs. This automation workflow scrapes Google Maps search results, visits each business website, and extracts email addresses for lead generation and outreach campaigns.

## 🚀 Features

- **No API costs** - Direct HTML scraping approach
- **Intelligent rate limiting** - Built-in delays prevent IP blocking
- **Email validation** - Filters out invalid emails and file extensions
- **Duplicate removal** - Ensures clean, unique email lists
- **Export ready** - Direct integration with Google Sheets
- **Error handling** - Continues processing even if individual sites fail
- **Scalable batching** - Process large lists efficiently

## 📋 Prerequisites

- n8n workflow automation platform
- Google Sheets account (for data export)
- Stable internet connection

## 🏗️ Workflow Architecture

### Step 1: Google Maps Data Extraction
- **Function**: Scrapes Google Maps search results
- **Input**: Search query (e.g., "Calgary dentists")
- **Output**: Raw HTML containing business listings and website URLs
- **Method**: Direct HTTP request to Google Maps search URL

### Step 2: Website URL Processing
- **Extract URLs**: Uses regex to find all website URLs in the HTML
- **Filter domains**: Removes Google-related URLs (google.com, gstatic, etc.)
- **Remove duplicates**: Eliminates duplicate websites
- **Batch limiting**: Controls processing size for testing

### Step 3: Smart Website Scraping
- **Sequential processing**: Visits each website individually
- **Rate limiting**: Built-in delays between requests
- **Error handling**: Continues if individual sites fail
- **IP protection**: Prevents blocking through smart timing

### Step 4: Email Extraction & Export
- **Email extraction**: Regex pattern finds valid email addresses
- **Content filtering**: Removes results with no emails found
- **Data splitting**: Converts email arrays to individual records
- **Final deduplication**: Ensures unique email list
- **Export**: Saves to Google Sheets for easy access

## ⚙️ Setup Instructions

### 1. Import Workflow
1. Copy the workflow JSON
2. Import into your n8n instance
3. Activate the workflow

### 2. Configure Google Sheets
1. Create a new Google Sheet
2. Add a column header "emails"
3. Update the Google Sheets node with your sheet ID
4. Ensure n8n has Google Sheets permissions

### 3. Customize Search Query
1. Open the "Scrape Google Maps" node
2. Replace the URL with your target search:
   ```
   https://www.google.com/maps/search/[LOCATION]+[BUSINESS_TYPE]
   ```
   Example: `https://www.google.com/maps/search/miami+restaurants`

### 4. Adjust Processing Limits
- **For testing**: Keep the Limit node at 10 items
- **For production**: Increase or remove the limit
- **Batch size**: Modify the "Loop Over Items" batch size as needed

## 🎯 Usage

1. **Start the workflow**: Click "Test workflow" or set up a trigger
2. **Monitor progress**: Watch the workflow process each step
3. **Check results**: View extracted emails in your Google Sheet
4. **Verify data**: Review and validate the collected emails

## 🔧 Configuration Options

### Search Parameters
- **Location**: Any city, region, or area
- **Business type**: Dentists, restaurants, lawyers, etc.
- **Combined queries**: "Calgary dental clinics" or "Miami Italian restaurants"

### Processing Limits
```json
"maxItems": 10  // Adjust in Limit node for testing
```

### Wait Times
- **Between sites**: 1 second (adjustable in Wait nodes)
- **Between batches**: Default timing (modify as needed)

### Email Regex Pattern
```javascript
/[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.(?!jpeg|jpg|png|gif|webp|svg)[a-zA-Z]{2,}/g
```
This pattern excludes image file extensions and validates proper email format.

## 📊 Expected Output

The workflow generates a clean list of business emails with the following characteristics:

- **Valid format**: Proper email address structure
- **No duplicates**: Each email appears only once
- **Business focused**: Filtered from actual business websites
- **Export ready**: Formatted for immediate use in outreach tools

## ⚠️ Important Considerations

### Rate Limiting
- **Essential for scale**: The built-in delays prevent IP blocking
- **Adjust timing**: Increase wait times if experiencing blocks
- **Monitor performance**: Watch for failed requests

### Legal Compliance
- **Respect robots.txt**: Check website scraping policies
- **GDPR compliance**: Ensure proper data handling
- **CAN-SPAM compliance**: Follow email marketing regulations
- **Terms of service**: Review Google Maps terms of use

### Best Practices
- **Start small**: Test with limited results first
- **Verify emails**: Validate emails before outreach
- **Respect websites**: Don't overwhelm target sites
- **Update regularly**: Refresh your email lists periodically

## 🔍 Troubleshooting

### Common Issues

**No emails found**
- Check if websites are loading properly
- Verify the email regex pattern
- Ensure sites aren't blocking scraping

**IP blocking**
- Increase wait times between requests
- Reduce batch sizes
- Use VPN or rotate IP addresses

**Google Sheets errors**
- Verify sheet permissions
- Check sheet ID in configuration
- Ensure proper column headers

**Workflow timeouts**
- Reduce processing batch size
- Increase node timeout limits
- Split large jobs into smaller batches

## 🚀 Optimization Tips

1. **Batch processing**: Start with small batches and scale up
2. **Error monitoring**: Check node logs for failed requests
3. **Data quality**: Regularly review extracted emails for accuracy
4. **Performance tuning**: Adjust wait times based on success rates

## 📈 Scaling for Production

For larger-scale operations:

1. **Remove/increase limits**: Modify the Limit node
2. **Implement retry logic**: Add error handling for failed requests
3. **Database storage**: Consider storing results in a database
4. **Monitoring**: Set up alerts for workflow failures
5. **Backup processing**: Save intermediate results regularly

## 🎯 Use Cases

- **Lead generation**: Build prospect lists for sales outreach
- **Market research**: Identify businesses in specific sectors
- **Competitor analysis**: Map business landscapes in target areas
- **Partnership outreach**: Find potential business partners
- **Local marketing**: Target businesses in specific geographic areas

## 📞 Support

For workflow customization or scaling assistance, consider:
- Reviewing n8n documentation
- Testing with small datasets first
- Implementing proper error handling
- Following web scraping best practices

---

**Note**: This workflow is designed for legitimate business purposes. Always ensure compliance with applicable laws and website terms of service when scraping data.
