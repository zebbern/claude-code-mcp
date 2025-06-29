# Browserbase MCP

## Overview
Browserbase MCP provides enterprise-grade browser infrastructure for AI agents through the Model Context Protocol. This service offers reliable, high-performance headless browsers at scale, enabling AI agents to interact with web applications, perform automated testing, web scraping, and complex browser-based workflows. Browserbase eliminates the complexity of managing browser infrastructure while providing advanced features like session persistence, proxy support, and comprehensive monitoring.

## Installation

### Prerequisites
- Browserbase account and API key
- Claude Desktop application
- Node.js 16+ or Python 3.8+
- Understanding of web automation concepts
- Basic knowledge of browser developer tools

### Install Steps

#### Option 1: Official Browserbase MCP Server
```bash
git clone https://github.com/browserbase/mcp-server-browserbase.git
cd mcp-server-browserbase
npm install
```

#### Option 2: NPM Package
```bash
npm install @browserbase/mcp-server
```

#### Option 3: Python Implementation
```bash
pip install browserbase-mcp
```

#### Option 4: Docker Container
```bash
docker run -d --name browserbase-mcp \
  -e BROWSERBASE_API_KEY=your-api-key \
  -e BROWSERBASE_PROJECT_ID=your-project-id \
  browserbase/mcp-server
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "browserbase": {
      "command": "npx",
      "args": [
        "@browserbase/mcp-server"
      ],
      "env": {
        "BROWSERBASE_API_KEY": "your-api-key",
        "BROWSERBASE_PROJECT_ID": "your-project-id"
      }
    }
  }
}
```

### Browserbase Project Configuration
```json
{
  "browserbase_config": {
    "project_id": "your-project-id",
    "api_key": "your-api-key",
    "default_settings": {
      "browser": "chromium",
      "viewport": {"width": 1920, "height": 1080},
      "timeout": 30000,
      "wait_for_selector_timeout": 10000,
      "navigation_timeout": 30000
    },
    "session_settings": {
      "persist_session": true,
      "session_timeout": "1h",
      "max_concurrent_sessions": 10,
      "auto_cleanup": true
    }
  }
}
```

### Advanced Configuration
```json
{
  "browserbase_advanced": {
    "browser_settings": {
      "user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36",
      "locale": "en-US",
      "timezone": "America/New_York",
      "geolocation": {"latitude": 40.7128, "longitude": -74.0060},
      "permissions": ["geolocation", "notifications", "camera", "microphone"]
    },
    "proxy_settings": {
      "enabled": true,
      "type": "residential",
      "rotation": "per_request",
      "countries": ["US", "UK", "CA"],
      "sticky_session": true
    },
    "stealth_settings": {
      "enabled": true,
      "hide_webdriver": true,
      "randomize_viewport": true,
      "randomize_user_agent": true,
      "block_resources": ["images", "fonts", "stylesheets"]
    },
    "monitoring": {
      "screenshots": true,
      "video_recording": true,
      "performance_metrics": true,
      "console_logs": true,
      "network_logs": true
    }
  }
}
```

## Usage Examples

### Basic Web Navigation
```
# Navigate to websites
Navigate to "https://example.com" and take a screenshot.

# Page interactions
Click the "Sign In" button on the current page.

# Form filling
Fill the email field with "user@example.com" and password field with "password123".

# Element interaction
Wait for the element with selector ".loading-spinner" to disappear, then click "Submit".

# Data extraction
Extract all product names and prices from the e-commerce listing page.
```

### Advanced Automation
```
# Multi-step workflows
1. Navigate to login page
2. Fill credentials and submit
3. Navigate to dashboard
4. Extract user profile information
5. Take screenshot of dashboard

# Dynamic content handling
Wait for the AJAX content to load, then extract the dynamically generated table data.

# File downloads
Click the "Download Report" button and wait for the file to download completely.

# Modal interactions
Handle the popup modal by clicking "Accept Cookies" and then proceed with navigation.

# Infinite scroll
Scroll down the page multiple times to load all content, then extract all article titles.
```

### E-commerce Automation
```
# Product research
Navigate to Amazon, search for "wireless headphones", and extract the top 10 products with prices and ratings.

# Price monitoring
Check the current price of a specific product and compare it with the historical price data.

# Inventory tracking
Monitor product availability across multiple e-commerce sites and alert when back in stock.

# Competitive analysis
Extract product information, pricing, and reviews from competitor websites.

# Cart automation
Add specific products to cart, proceed to checkout, and capture the total price before payment.
```

### Testing and QA
```
# Functional testing
Test the complete user registration flow from signup to email verification.

# Cross-browser testing
Run the same test suite across Chrome, Firefox, and Safari browsers.

# Performance testing
Measure page load times, Core Web Vitals, and identify performance bottlenecks.

# Accessibility testing
Check for accessibility violations and generate a compliance report.

# Visual regression testing
Compare current page screenshots with baseline images to detect visual changes.
```

### Data Collection
```
# Web scraping
Extract structured data from news websites, job boards, or real estate listings.

# Social media monitoring
Monitor social media platforms for brand mentions and sentiment analysis.

# Market research
Collect pricing data, product specifications, and customer reviews from multiple sources.

# Lead generation
Extract contact information from business directories and professional networks.

# Content aggregation
Collect articles, blog posts, and news from multiple sources for content curation.
```

## Features

### Core Browser Capabilities
- **Multi-Browser Support**: Chrome, Firefox, Safari, and Edge browsers
- **Headless Operation**: Run browsers without GUI for better performance
- **Session Management**: Persistent sessions with state preservation
- **Viewport Control**: Customizable browser window sizes and device emulation
- **Network Control**: Request/response interception and modification

### Advanced Automation Features
- **Smart Waiting**: Intelligent waiting for elements, network requests, and page loads
- **Element Interaction**: Click, type, hover, drag-and-drop operations
- **Form Handling**: Automated form filling and submission
- **File Operations**: Upload and download file handling
- **JavaScript Execution**: Custom JavaScript code execution in browser context

### Enterprise Features
- **Scalable Infrastructure**: Auto-scaling browser instances based on demand
- **Global Proxy Network**: Residential and datacenter proxies worldwide
- **Session Recording**: Video recording and screenshot capture
- **Performance Monitoring**: Real-time performance metrics and alerts
- **Compliance**: GDPR, SOC 2, and enterprise security standards

### Stealth and Anti-Detection
- **Stealth Mode**: Advanced anti-detection techniques
- **User Agent Rotation**: Randomized user agents and browser fingerprints
- **Proxy Rotation**: Automatic IP rotation and geolocation spoofing
- **CAPTCHA Handling**: Integrated CAPTCHA solving capabilities
- **Bot Detection Evasion**: Advanced techniques to bypass bot detection

### Integration Capabilities
- **API Integration**: RESTful API for programmatic access
- **Webhook Support**: Real-time notifications and event triggers
- **Third-party Tools**: Integration with testing frameworks and CI/CD pipelines
- **Data Export**: Multiple formats for data export and analysis
- **Monitoring Dashboards**: Real-time monitoring and analytics

## Requirements

### System Requirements
- **Operating System**: Any OS with Node.js or Python support
- **Memory**: 2GB RAM minimum, 4GB+ recommended
- **Network**: Stable internet connection with good bandwidth
- **Storage**: 1GB+ for temporary files and screenshots
- **API Access**: Valid Browserbase account and API credentials

### Browserbase Account Requirements
```javascript
// Account tier requirements
const account_tiers = {
  "starter": {
    "concurrent_sessions": 3,
    "monthly_sessions": 1000,
    "session_duration": "30m",
    "features": ["basic_automation", "screenshots"]
  },
  "professional": {
    "concurrent_sessions": 10,
    "monthly_sessions": 10000,
    "session_duration": "2h",
    "features": ["advanced_automation", "video_recording", "proxy_support"]
  },
  "enterprise": {
    "concurrent_sessions": "unlimited",
    "monthly_sessions": "unlimited",
    "session_duration": "unlimited",
    "features": ["all_features", "dedicated_support", "custom_integrations"]
  }
};
```

### Performance Requirements
- Minimum session timeout: 30 seconds
- Maximum session duration: 2 hours (varies by plan)
- Concurrent session limits based on subscription tier
- API rate limits: 100 requests per minute (varies by plan)
- Screenshot/video storage: 30 days retention

## Security Considerations

### Best Practices
- **API Key Security**: Secure storage and rotation of API keys
- **Data Privacy**: Ensure compliance with data protection regulations
- **Session Isolation**: Proper session isolation and cleanup
- **Network Security**: Use HTTPS for all API communications
- **Access Control**: Implement proper access controls and authentication

### Secure Configuration
```json
{
  "security": {
    "api_keys": {
      "encryption": "AES-256",
      "rotation_period": "90d",
      "storage": "environment_variables"
    },
    "sessions": {
      "isolation": "complete",
      "cleanup": "automatic",
      "data_retention": "minimal",
      "encryption": "in_transit_and_at_rest"
    },
    "network": {
      "https_only": true,
      "certificate_validation": true,
      "proxy_authentication": "required",
      "rate_limiting": "enabled"
    }
  }
}
```

### Privacy Protection
```javascript
// Privacy protection measures
const privacy_protection = {
  "data_minimization": "Collect only necessary data",
  "session_cleanup": "Automatic cleanup after session end",
  "no_persistent_storage": "No data stored beyond session duration",
  "encrypted_transmission": "All data encrypted in transit",
  "compliance": ["GDPR", "CCPA", "SOC2"]
};
```

## Troubleshooting

### Common Issues

#### Session Creation Problems
**Problem**: Cannot create browser session
**Solution**:
```bash
# Check API credentials
curl -X GET "https://api.browserbase.com/v1/sessions" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "X-BB-Project-Id: YOUR_PROJECT_ID"

# Verify account limits
curl -X GET "https://api.browserbase.com/v1/usage" \
  -H "Authorization: Bearer YOUR_API_KEY"

# Test session creation
curl -X POST "https://api.browserbase.com/v1/sessions" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "X-BB-Project-Id: YOUR_PROJECT_ID" \
  -H "Content-Type: application/json" \
  -d '{"browser": "chromium"}'
```

#### Element Interaction Issues
**Problem**: Cannot find or interact with elements
**Solution**:
- Use more specific selectors (CSS, XPath)
- Implement proper waiting strategies
- Check for dynamic content loading
- Verify element visibility and interactability

#### Performance Issues
**Problem**: Slow page loading or timeouts
**Solution**:
```javascript
// Optimize browser settings
const optimization_settings = {
  "block_resources": ["images", "fonts", "stylesheets"],
  "disable_javascript": false,
  "viewport": {"width": 1280, "height": 720},
  "timeout": 15000,
  "wait_until": "networkidle0"
};
```

#### Proxy and Geolocation Issues
**Problem**: Proxy not working or incorrect geolocation
**Solution**:
- Verify proxy configuration and credentials
- Check proxy server status and availability
- Test geolocation settings with location-aware websites
- Ensure proxy type matches requirements (residential vs datacenter)

### Diagnostic Tools
```bash
# Session status check
browserbase-mcp --session-status --session-id <id>

# Performance metrics
browserbase-mcp --performance --session-id <id>

# Network logs
browserbase-mcp --network-logs --session-id <id>

# Screenshot capture
browserbase-mcp --screenshot --session-id <id> --output screenshot.png
```

## Advanced Configuration

### Custom Browser Profiles
```json
{
  "browser_profiles": {
    "mobile_chrome": {
      "browser": "chromium",
      "viewport": {"width": 375, "height": 667},
      "user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 14_7_1 like Mac OS X)",
      "device_scale_factor": 2,
      "is_mobile": true,
      "has_touch": true
    },
    "desktop_firefox": {
      "browser": "firefox",
      "viewport": {"width": 1920, "height": 1080},
      "user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:91.0) Gecko/20100101 Firefox/91.0",
      "locale": "en-US",
      "timezone": "America/New_York"
    }
  }
}
```

### Automation Workflows
```python
# Complex automation workflow
class BrowserbaseWorkflow:
    def __init__(self, api_key, project_id):
        self.api_key = api_key
        self.project_id = project_id
        self.session = None
    
    async def create_session(self, config=None):
        """Create a new browser session with optional configuration"""
        default_config = {
            "browser": "chromium",
            "viewport": {"width": 1920, "height": 1080},
            "timeout": 30000
        }
        
        if config:
            default_config.update(config)
        
        self.session = await self.browserbase_client.create_session(default_config)
        return self.session
    
    async def navigate_and_extract(self, url, selectors):
        """Navigate to URL and extract data using provided selectors"""
        await self.session.navigate(url)
        await self.session.wait_for_load_state("networkidle")
        
        results = {}
        for key, selector in selectors.items():
            elements = await self.session.query_selector_all(selector)
            results[key] = [await el.text_content() for el in elements]
        
        return results
    
    async def perform_actions(self, actions):
        """Perform a sequence of browser actions"""
        for action in actions:
            action_type = action["type"]
            
            if action_type == "click":
                await self.session.click(action["selector"])
            elif action_type == "type":
                await self.session.fill(action["selector"], action["text"])
            elif action_type == "wait":
                await self.session.wait_for_selector(action["selector"])
            elif action_type == "screenshot":
                await self.session.screenshot(action["path"])
    
    async def cleanup(self):
        """Clean up session resources"""
        if self.session:
            await self.session.close()
```

### Performance Optimization
```python
# Performance optimization strategies
class PerformanceOptimizer:
    def __init__(self):
        self.optimization_rules = {
            "block_resources": ["image", "font", "stylesheet"],
            "cache_strategy": "aggressive",
            "compression": "gzip",
            "timeout_strategy": "adaptive"
        }
    
    def optimize_for_speed(self, session_config):
        """Optimize session configuration for speed"""
        optimized_config = session_config.copy()
        
        # Block unnecessary resources
        optimized_config["block_resources"] = self.optimization_rules["block_resources"]
        
        # Reduce viewport size for faster rendering
        optimized_config["viewport"] = {"width": 1280, "height": 720}
        
        # Disable images and CSS for data extraction
        optimized_config["load_images"] = False
        optimized_config["load_css"] = False
        
        # Set aggressive timeouts
        optimized_config["timeout"] = 15000
        optimized_config["wait_until"] = "domcontentloaded"
        
        return optimized_config
    
    def optimize_for_accuracy(self, session_config):
        """Optimize session configuration for accuracy"""
        optimized_config = session_config.copy()
        
        # Enable all resources for complete page rendering
        optimized_config["block_resources"] = []
        optimized_config["load_images"] = True
        optimized_config["load_css"] = True
        
        # Use longer timeouts for complex pages
        optimized_config["timeout"] = 60000
        optimized_config["wait_until"] = "networkidle0"
        
        # Enable JavaScript for dynamic content
        optimized_config["javascript_enabled"] = True
        
        return optimized_config
```

### Monitoring and Analytics
```python
# Session monitoring and analytics
class SessionMonitor:
    def __init__(self, session_id):
        self.session_id = session_id
        self.metrics = {}
    
    def track_performance(self):
        """Track session performance metrics"""
        self.metrics["page_load_time"] = self.get_page_load_time()
        self.metrics["dom_content_loaded"] = self.get_dom_content_loaded_time()
        self.metrics["first_contentful_paint"] = self.get_fcp_time()
        self.metrics["largest_contentful_paint"] = self.get_lcp_time()
        self.metrics["cumulative_layout_shift"] = self.get_cls_score()
    
    def track_errors(self):
        """Track JavaScript errors and console logs"""
        self.metrics["javascript_errors"] = self.get_js_errors()
        self.metrics["console_warnings"] = self.get_console_warnings()
        self.metrics["network_errors"] = self.get_network_errors()
    
    def generate_report(self):
        """Generate comprehensive session report"""
        return {
            "session_id": self.session_id,
            "performance_metrics": self.metrics,
            "recommendations": self.get_optimization_recommendations(),
            "timestamp": datetime.now().isoformat()
        }
```

## Workflow Examples

### E-commerce Price Monitoring
```python
# E-commerce price monitoring workflow
price_monitoring_workflow = {
    "setup": {
        "products": [
            {"name": "iPhone 14", "urls": ["amazon.com", "bestbuy.com", "apple.com"]},
            {"name": "MacBook Pro", "urls": ["amazon.com", "bestbuy.com", "apple.com"]}
        ],
        "schedule": "daily",
        "alert_threshold": 0.05  # 5% price change
    },
    "extraction": {
        "selectors": {
            "amazon": {"price": ".a-price-whole", "title": "#productTitle"},
            "bestbuy": {"price": ".sr-only", "title": ".sku-title"},
            "apple": {"price": ".current_price", "title": ".pd-title"}
        }
    },
    "analysis": {
        "price_comparison": True,
        "historical_tracking": True,
        "trend_analysis": True,
        "alert_conditions": ["price_drop", "back_in_stock", "new_variant"]
    }
}
```

### Social Media Monitoring
```python
# Social media monitoring workflow
social_monitoring_workflow = {
    "platforms": {
        "twitter": {
            "search_terms": ["brand_name", "#brand_hashtag"],
            "sentiment_analysis": True,
            "influencer_tracking": True
        },
        "linkedin": {
            "company_mentions": True,
            "industry_discussions": True,
            "competitor_analysis": True
        },
        "reddit": {
            "subreddit_monitoring": ["r/technology", "r/business"],
            "keyword_alerts": True,
            "community_sentiment": True
        }
    },
    "analysis": {
        "sentiment_scoring": "automatic",
        "trend_detection": True,
        "alert_thresholds": {
            "negative_sentiment": 0.3,
            "mention_volume": 100,
            "viral_potential": 0.8
        }
    }
}
```

### Competitive Intelligence
```python
# Competitive intelligence workflow
competitive_intelligence_workflow = {
    "competitors": [
        {"name": "Competitor A", "website": "competitor-a.com"},
        {"name": "Competitor B", "website": "competitor-b.com"}
    ],
    "monitoring_areas": {
        "product_updates": {
            "pages": ["/products", "/features", "/pricing"],
            "change_detection": True,
            "screenshot_comparison": True
        },
        "content_strategy": {
            "blog_monitoring": True,
            "social_media_tracking": True,
            "seo_analysis": True
        },
        "pricing_strategy": {
            "price_tracking": True,
            "promotion_detection": True,
            "package_comparison": True
        }
    },
    "reporting": {
        "frequency": "weekly",
        "format": "dashboard",
        "stakeholders": ["marketing", "product", "strategy"]
    }
}
```

## Integration with Other MCPs

### With Data Analytics MCPs
```
# Business intelligence integration
1. Use Browserbase MCP for web data collection
2. Use analytics MCPs to process and analyze collected data
3. Generate insights and reports from web-scraped information
4. Create automated dashboards with real-time web data
```

### With Notification MCPs
```
# Alert and notification integration
1. Use Browserbase MCP to monitor websites for changes
2. Use notification MCPs to send alerts when changes are detected
3. Integrate with email, Slack, or SMS for immediate notifications
4. Create escalation workflows for critical changes
```

### With Database MCPs
```
# Data storage and management integration
1. Use Browserbase MCP to extract structured data from websites
2. Use database MCPs to store and organize collected data
3. Implement data deduplication and quality checks
4. Create historical data analysis and trend reporting
```

## Performance Optimization

### Session Management
```python
# Efficient session management
class SessionManager:
    def __init__(self, max_concurrent=5):
        self.max_concurrent = max_concurrent
        self.active_sessions = {}
        self.session_pool = []
    
    async def get_session(self, config=None):
        """Get an available session or create a new one"""
        if self.session_pool:
            session = self.session_pool.pop()
            await session.reset()
            return session
        
        if len(self.active_sessions) < self.max_concurrent:
            session = await self.create_new_session(config)
            self.active_sessions[session.id] = session
            return session
        
        # Wait for a session to become available
        return await self.wait_for_available_session()
    
    async def release_session(self, session):
        """Release a session back to the pool"""
        await session.clear_data()
        self.session_pool.append(session)
    
    async def cleanup_all_sessions(self):
        """Clean up all active sessions"""
        for session in self.active_sessions.values():
            await session.close()
        self.active_sessions.clear()
        self.session_pool.clear()
```

### Resource Optimization
```python
# Resource usage optimization
class ResourceOptimizer:
    def __init__(self):
        self.optimization_profiles = {
            "data_extraction": {
                "block_resources": ["image", "font", "stylesheet", "media"],
                "javascript_enabled": True,
                "wait_strategy": "domcontentloaded"
            },
            "visual_testing": {
                "block_resources": [],
                "javascript_enabled": True,
                "wait_strategy": "networkidle0"
            },
            "performance_testing": {
                "block_resources": [],
                "javascript_enabled": True,
                "metrics_collection": True
            }
        }
    
    def get_optimized_config(self, use_case):
        """Get optimized configuration for specific use case"""
        base_config = {
            "browser": "chromium",
            "viewport": {"width": 1920, "height": 1080},
            "timeout": 30000
        }
        
        if use_case in self.optimization_profiles:
            base_config.update(self.optimization_profiles[use_case])
        
        return base_config
```

### Caching Strategies
```python
# Intelligent caching for repeated operations
class BrowserbaseCache:
    def __init__(self, redis_client):
        self.redis = redis_client
        self.cache_ttl = {
            "page_content": 3600,  # 1 hour
            "screenshots": 86400,  # 24 hours
            "extracted_data": 1800  # 30 minutes
        }
    
    def cache_page_content(self, url, content):
        """Cache page content with URL-based key"""
        key = f"page_content:{hashlib.md5(url.encode()).hexdigest()}"
        self.redis.setex(key, self.cache_ttl["page_content"], content)
    
    def get_cached_content(self, url):
        """Retrieve cached page content"""
        key = f"page_content:{hashlib.md5(url.encode()).hexdigest()}"
        return self.redis.get(key)
    
    def cache_extracted_data(self, url, selectors, data):
        """Cache extracted data with URL and selector hash"""
        selector_hash = hashlib.md5(str(selectors).encode()).hexdigest()
        key = f"extracted_data:{hashlib.md5(url.encode()).hexdigest()}:{selector_hash}"
        self.redis.setex(key, self.cache_ttl["extracted_data"], json.dumps(data))
```

## Links

- [Browserbase MCP Repository](https://github.com/browserbase/mcp-server-browserbase)
- [Browserbase Official Documentation](https://docs.browserbase.com/)
- [Browserbase API Reference](https://docs.browserbase.com/api-reference)
- [Browserbase Dashboard](https://www.browserbase.com/dashboard)
- [Browserbase Pricing](https://www.browserbase.com/pricing)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [Browserbase MCP Community](https://github.com/browserbase/mcp-server-browserbase/discussions)
- [Browserbase Discord](https://discord.gg/browserbase)
- [Browserbase Examples](https://github.com/browserbase/mcp-server-browserbase/tree/main/examples)
- [Web Automation Best Practices](https://docs.browserbase.com/guides/best-practices)
- [Browserbase Blog](https://www.browserbase.com/blog)
- [MCP Discord](https://discord.gg/mcp)

