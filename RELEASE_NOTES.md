# Trivy EPSS Plugin v0.0.1

## Overview
First release of the Trivy EPSS Plugin, a tool that enriches Trivy vulnerability scan results with EPSS (Exploit Prediction Scoring System) data from FIRST.org.

## Features
- Seamless integration with Trivy vulnerability scanner
- Automatic EPSS score retrieval for all detected CVEs
- Enrichment of vulnerability reports with:
  - EPSS scores
  - EPSS percentiles
  - Score calculation dates
- Efficient batch processing of CVEs
- Rate limiting support for API requests
- Graceful handling of CVEs without EPSS scores

## Technical Details
- Uses FIRST.org's EPSS API (v1)
- Processes CVEs in batches of 100
- Implements 100ms delay between batches to respect API limits
- Adds EPSS data in Trivy's custom fields format

## Usage
The plugin adds the following fields to each vulnerability in the Trivy report:
```bash
trivy image --format json your-image | trivy-plugin-epss > enriched-results.json
```

## Output Format

```json
{
"Custom": {
"epss_score": 0.12345,
"epss_percentile": 0.67890,
"epss_date": "2024-12-11",
"epss_source": "FIRST.org"
}
}
```
