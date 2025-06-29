# WhatsApp MCP

## Overview
WhatsApp MCP enables Claude AI to interact with WhatsApp messaging platform through the Model Context Protocol. This integration allows for automated message sending, conversation analysis, contact management, group administration, and business communication workflows. The MCP provides secure, API-based access to WhatsApp functionality without requiring browser automation or unofficial methods.

## Installation

### Prerequisites
- WhatsApp Business API access or WhatsApp Web session
- Claude Desktop application
- Node.js 16+ or Python 3.8+
- Valid phone number for WhatsApp registration
- Understanding of WhatsApp's terms of service and API limitations

### Install Steps

#### Option 1: Official WhatsApp Business API
```bash
git clone https://github.com/lharries/whatsapp-mcp.git
cd whatsapp-mcp
npm install
```

#### Option 2: Python Implementation
```bash
pip install whatsapp-mcp-server
```

#### Option 3: GreenAPI Integration
```bash
git clone https://github.com/msaelices/whatsapp-mcp-server.git
cd whatsapp-mcp-server
pip install -r requirements.txt
```

#### Option 4: Docker Container
```bash
docker run -d --name whatsapp-mcp \
  -e WHATSAPP_API_KEY=your-api-key \
  -e WHATSAPP_INSTANCE_ID=your-instance-id \
  whatsapp-mcp-server
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "whatsapp": {
      "command": "node",
      "args": [
        "/path/to/whatsapp-mcp/dist/index.js",
        "--api-key", "your-whatsapp-api-key",
        "--instance-id", "your-instance-id"
      ]
    }
  }
}
```

### WhatsApp Business API Configuration
```json
{
  "whatsapp_config": {
    "api_version": "v17.0",
    "phone_number_id": "your-phone-number-id",
    "business_account_id": "your-business-account-id",
    "access_token": "your-access-token",
    "webhook_verify_token": "your-webhook-token",
    "webhook_url": "https://your-domain.com/webhook"
  }
}
```

### GreenAPI Configuration
```json
{
  "greenapi_config": {
    "instance_id": "your-instance-id",
    "api_token": "your-api-token",
    "api_url": "https://api.green-api.com",
    "webhook_url": "https://your-domain.com/webhook",
    "settings": {
      "webhookUrl": "https://your-domain.com/webhook",
      "delaySendMessagesMilliseconds": 1000,
      "markIncomingMessagesReaded": "yes"
    }
  }
}
```

### Advanced Configuration
```json
{
  "whatsapp_advanced": {
    "message_settings": {
      "auto_read_messages": true,
      "typing_indicator": true,
      "delivery_receipts": true,
      "read_receipts": true,
      "last_seen": false
    },
    "rate_limiting": {
      "messages_per_minute": 60,
      "messages_per_hour": 1000,
      "burst_limit": 10,
      "cooldown_period": "5m"
    },
    "security": {
      "encryption": "end_to_end",
      "message_retention": "30d",
      "audit_logging": true,
      "access_control": "role_based"
    },
    "features": {
      "group_management": true,
      "broadcast_lists": true,
      "status_updates": true,
      "media_handling": true,
      "contact_sync": true
    }
  }
}
```

## Usage Examples

### Basic Messaging
```
# Send text messages
Send a message "Hello, how are you today?" to contact John Smith.

# Send messages to groups
Send "Meeting reminder: 3 PM today" to the "Project Team" group.

# Send media messages
Send the image "project_update.png" with caption "Latest progress update" to the client group.

# Send documents
Send the PDF file "proposal.pdf" to contact Sarah Johnson with message "Please review this proposal".

# Send location
Send current location to contact "Emergency Contact" with message "I'm here".
```

### Contact Management
```
# Add new contacts
Add contact with name "Alice Cooper" and phone number "+1234567890".

# Update contact information
Update contact "Bob Wilson" with new phone number "+0987654321".

# Search contacts
Find all contacts with name containing "Smith".

# Get contact details
Retrieve full contact information for "Marketing Team Lead".

# Block/unblock contacts
Block contact "+1234567890" and add to blocked list.
```

### Group Management
```
# Create groups
Create a new group called "Development Team" with members Alice, Bob, and Charlie.

# Add/remove members
Add contact "David Lee" to group "Project Alpha".
Remove contact "Eve Brown" from group "Marketing Team".

# Update group settings
Change group "Sales Team" description to "Q4 Sales Planning and Updates".

# Group administration
Make contact "Alice Cooper" an admin of group "Development Team".

# Leave groups
Leave group "Old Project Team" and notify members.
```

### Business Communication
```
# Customer support
Respond to customer inquiry about order status with tracking information.

# Appointment scheduling
Send appointment confirmation to client for "Tomorrow 2 PM - Strategy Meeting".

# Order notifications
Send order confirmation with details to customer who just made a purchase.

# Marketing campaigns
Send promotional message about new product launch to subscriber list.

# Follow-up messages
Send follow-up message to leads who haven't responded in 3 days.
```

### Automated Workflows
```
# Auto-responders
Set up automatic reply "Thanks for your message. We'll respond within 24 hours" for after-hours messages.

# Message scheduling
Schedule message "Happy Birthday!" to be sent to contact "Mom" tomorrow at 9 AM.

# Conditional responses
If message contains "support" or "help", automatically forward to support team.

# Message analysis
Analyze conversation sentiment and flag negative interactions for review.

# Bulk operations
Send personalized messages to all contacts in "VIP Customers" group.
```

## Features

### Core Messaging Capabilities
- **Text Messaging**: Send and receive text messages with formatting
- **Media Sharing**: Images, videos, documents, audio messages
- **Location Sharing**: Send and receive location information
- **Contact Cards**: Share contact information as vCards
- **Voice Messages**: Send and receive voice notes

### Advanced Communication Features
- **Message Reactions**: React to messages with emojis
- **Message Replies**: Reply to specific messages in conversations
- **Message Forwarding**: Forward messages between contacts and groups
- **Message Deletion**: Delete messages for everyone or just yourself
- **Message Editing**: Edit sent messages (where supported)

### Group Management
- **Group Creation**: Create and configure new groups
- **Member Management**: Add, remove, and manage group members
- **Admin Controls**: Assign and manage group administrators
- **Group Settings**: Configure group description, picture, and permissions
- **Broadcast Lists**: Send messages to multiple contacts without creating groups

### Business Features
- **WhatsApp Business API**: Full business API integration
- **Message Templates**: Pre-approved message templates for business use
- **Customer Support**: Structured customer support workflows
- **Analytics**: Message delivery and engagement analytics
- **Automation**: Automated responses and workflow triggers

### Security and Privacy
- **End-to-End Encryption**: All messages encrypted by default
- **Two-Factor Authentication**: Enhanced account security
- **Privacy Controls**: Manage who can see your information
- **Message Backup**: Secure message backup and restore
- **Audit Logging**: Comprehensive activity logging for compliance

## Requirements

### System Requirements
- **Operating System**: Windows 10+, macOS 10.15+, or Linux
- **Memory**: 4GB RAM minimum, 8GB+ recommended
- **Storage**: 1GB+ available space for message cache
- **Network**: Stable internet connection for real-time messaging
- **Phone**: Valid phone number for WhatsApp registration

### API Requirements
```javascript
// WhatsApp Business API requirements
const api_requirements = {
  "business_verification": "required",
  "phone_number": "business_verified",
  "webhook_endpoint": "https_required",
  "rate_limits": {
    "messages_per_second": 20,
    "messages_per_minute": 1000,
    "messages_per_day": 100000
  },
  "compliance": ["GDPR", "CCPA", "WhatsApp_Commerce_Policy"]
};
```

### Development Requirements
- Node.js 16+ or Python 3.8+
- WhatsApp Business API access token
- Webhook endpoint for receiving messages
- SSL certificate for secure communication
- Understanding of WhatsApp's rate limits and policies

## Security Considerations

### Best Practices
- **API Key Security**: Secure storage and rotation of API keys
- **Webhook Security**: Verify webhook signatures and use HTTPS
- **Data Privacy**: Comply with data protection regulations
- **Rate Limiting**: Implement proper rate limiting to avoid blocks
- **Message Validation**: Validate all incoming and outgoing messages

### Secure Configuration
```json
{
  "security": {
    "api_keys": {
      "encryption": "AES-256",
      "rotation_period": "90d",
      "storage": "secure_vault"
    },
    "webhooks": {
      "signature_verification": true,
      "https_only": true,
      "ip_whitelist": ["52.25.0.0/16", "34.224.0.0/12"],
      "timeout": "30s"
    },
    "data_protection": {
      "message_encryption": "end_to_end",
      "data_retention": "as_required",
      "anonymization": "automatic",
      "audit_trail": "comprehensive"
    }
  }
}
```

### Privacy Protection
```javascript
// Privacy protection measures
const privacy_protection = {
  "data_minimization": "Collect only necessary data",
  "consent_management": "Explicit consent for data processing",
  "right_to_deletion": "Support data deletion requests",
  "data_portability": "Enable data export functionality",
  "breach_notification": "Immediate notification of security breaches"
};
```

## Troubleshooting

### Common Issues

#### Connection Problems
**Problem**: Cannot connect to WhatsApp API
**Solution**:
```bash
# Check API credentials
curl -X GET "https://graph.facebook.com/v17.0/me" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"

# Verify webhook endpoint
curl -X GET "https://your-domain.com/webhook?hub.verify_token=YOUR_VERIFY_TOKEN"

# Test phone number status
curl -X GET "https://graph.facebook.com/v17.0/YOUR_PHONE_NUMBER_ID" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

#### Message Delivery Issues
**Problem**: Messages not being delivered
**Solution**:
- Check recipient phone number format (+country_code_number)
- Verify message template approval status
- Review rate limiting and quota usage
- Confirm recipient has WhatsApp installed and active

#### Webhook Problems
**Problem**: Not receiving incoming messages
**Solution**:
```python
# Verify webhook configuration
import requests

def verify_webhook():
    webhook_url = "https://your-domain.com/webhook"
    verify_token = "your-verify-token"
    
    response = requests.get(f"{webhook_url}?hub.verify_token={verify_token}")
    print(f"Webhook status: {response.status_code}")
    return response.status_code == 200
```

#### Rate Limiting Issues
**Problem**: API requests being throttled
**Solution**:
- Implement exponential backoff for retries
- Monitor rate limit headers in API responses
- Distribute message sending over time
- Use message queuing for bulk operations

### Diagnostic Tools
```bash
# API health check
whatsapp-mcp --health-check

# Message delivery status
whatsapp-mcp --check-delivery --message-id <id>

# Webhook testing
whatsapp-mcp --test-webhook --url <webhook-url>

# Rate limit monitoring
whatsapp-mcp --rate-limits --detailed
```

## Advanced Configuration

### Message Templates
```json
{
  "message_templates": {
    "appointment_reminder": {
      "name": "appointment_reminder",
      "language": "en_US",
      "category": "UTILITY",
      "components": [
        {
          "type": "BODY",
          "text": "Hi {{1}}, this is a reminder that you have an appointment on {{2}} at {{3}}."
        },
        {
          "type": "FOOTER",
          "text": "Reply STOP to opt out"
        }
      ]
    },
    "order_confirmation": {
      "name": "order_confirmation",
      "language": "en_US",
      "category": "TRANSACTIONAL",
      "components": [
        {
          "type": "HEADER",
          "format": "TEXT",
          "text": "Order Confirmation"
        },
        {
          "type": "BODY",
          "text": "Your order #{{1}} has been confirmed. Total: ${{2}}. Estimated delivery: {{3}}."
        }
      ]
    }
  }
}
```

### Automated Workflows
```python
# Automated customer support workflow
class CustomerSupportWorkflow:
    def __init__(self):
        self.keywords = {
            "support": ["help", "support", "issue", "problem"],
            "billing": ["bill", "payment", "charge", "invoice"],
            "technical": ["bug", "error", "not working", "broken"]
        }
    
    def process_message(self, message, sender):
        category = self.categorize_message(message)
        
        if category == "support":
            return self.handle_support_request(message, sender)
        elif category == "billing":
            return self.handle_billing_inquiry(message, sender)
        elif category == "technical":
            return self.handle_technical_issue(message, sender)
        else:
            return self.handle_general_inquiry(message, sender)
    
    def categorize_message(self, message):
        message_lower = message.lower()
        
        for category, keywords in self.keywords.items():
            if any(keyword in message_lower for keyword in keywords):
                return category
        
        return "general"
```

### Integration Patterns
```python
# CRM integration pattern
class CRMIntegration:
    def __init__(self, crm_api):
        self.crm_api = crm_api
    
    def sync_contact(self, whatsapp_contact):
        # Check if contact exists in CRM
        crm_contact = self.crm_api.find_contact(whatsapp_contact.phone)
        
        if crm_contact:
            # Update existing contact
            self.crm_api.update_contact(crm_contact.id, {
                "whatsapp_number": whatsapp_contact.phone,
                "last_whatsapp_activity": datetime.now()
            })
        else:
            # Create new contact
            self.crm_api.create_contact({
                "name": whatsapp_contact.name,
                "phone": whatsapp_contact.phone,
                "source": "whatsapp",
                "created_date": datetime.now()
            })
    
    def log_conversation(self, conversation):
        # Log conversation in CRM
        self.crm_api.create_activity({
            "type": "whatsapp_conversation",
            "contact_phone": conversation.contact,
            "messages": conversation.messages,
            "timestamp": conversation.timestamp
        })
```

## Workflow Examples

### Customer Service Automation
```python
# Customer service automation workflow
customer_service_workflow = {
    "initial_response": {
        "trigger": "new_message_from_unknown_contact",
        "action": "send_welcome_message",
        "template": "customer_service_welcome",
        "escalation": "human_agent_after_3_messages"
    },
    "issue_categorization": {
        "keywords": {
            "technical": ["app", "website", "login", "password"],
            "billing": ["payment", "charge", "refund", "invoice"],
            "shipping": ["delivery", "tracking", "address", "shipping"]
        },
        "auto_routing": True,
        "confidence_threshold": 0.8
    },
    "resolution_tracking": {
        "follow_up_after": "24h",
        "satisfaction_survey": True,
        "case_closure": "automatic_after_resolved"
    }
}
```

### Sales Lead Management
```python
# Sales lead management workflow
sales_workflow = {
    "lead_qualification": {
        "questions": [
            "What's your budget range?",
            "When are you looking to implement?",
            "What's your company size?",
            "Who's the decision maker?"
        ],
        "scoring": {
            "budget_qualified": 25,
            "timeline_qualified": 25,
            "authority_qualified": 25,
            "need_qualified": 25
        }
    },
    "nurturing_sequence": {
        "day_1": "welcome_and_value_proposition",
        "day_3": "case_study_relevant_to_industry",
        "day_7": "product_demo_invitation",
        "day_14": "pricing_and_packages",
        "day_21": "limited_time_offer"
    },
    "handoff_criteria": {
        "lead_score": ">75",
        "engagement_level": "high",
        "budget_confirmed": True,
        "timeline_within_quarter": True
    }
}
```

### Event Management
```python
# Event management workflow
event_workflow = {
    "registration": {
        "confirmation_message": "Thanks for registering! Event details: {{event_name}} on {{date}} at {{location}}",
        "reminder_schedule": ["7d", "1d", "2h"],
        "cancellation_policy": "24h_notice_required"
    },
    "updates": {
        "venue_changes": "immediate_notification",
        "schedule_updates": "24h_advance_notice",
        "weather_alerts": "automatic_if_outdoor_event"
    },
    "post_event": {
        "feedback_request": "24h_after_event",
        "photo_sharing": "event_gallery_link",
        "next_event_promotion": "1_week_after"
    }
}
```

## Integration with Other MCPs

### With CRM MCPs
```
# Customer relationship management integration
1. Use WhatsApp MCP for customer communication
2. Use CRM MCPs to sync contact information and conversation history
3. Track customer interactions across all channels
4. Automate follow-up sequences based on CRM data
```

### With Calendar MCPs
```
# Appointment scheduling integration
1. Use WhatsApp MCP for appointment requests
2. Use Calendar MCPs to check availability and book appointments
3. Send automated reminders via WhatsApp
4. Handle rescheduling and cancellations
```

### With E-commerce MCPs
```
# E-commerce integration
1. Use WhatsApp MCP for order notifications and customer support
2. Use E-commerce MCPs to access order and product information
3. Provide real-time order tracking via WhatsApp
4. Handle returns and exchanges through messaging
```

## Performance Optimization

### Message Queue Management
```python
# Message queue optimization
class MessageQueue:
    def __init__(self, max_rate=20):  # 20 messages per second
        self.max_rate = max_rate
        self.queue = []
        self.last_sent = 0
    
    def add_message(self, message):
        self.queue.append({
            "message": message,
            "timestamp": time.time(),
            "priority": message.get("priority", "normal")
        })
        
        # Sort by priority and timestamp
        self.queue.sort(key=lambda x: (x["priority"] == "high", -x["timestamp"]))
    
    def process_queue(self):
        current_time = time.time()
        
        if current_time - self.last_sent >= (1.0 / self.max_rate):
            if self.queue:
                message = self.queue.pop(0)
                self.send_message(message["message"])
                self.last_sent = current_time
```

### Caching Strategies
```python
# Contact and conversation caching
class WhatsAppCache:
    def __init__(self, redis_client):
        self.redis = redis_client
        self.contact_ttl = 3600  # 1 hour
        self.conversation_ttl = 86400  # 24 hours
    
    def cache_contact(self, phone, contact_data):
        key = f"contact:{phone}"
        self.redis.setex(key, self.contact_ttl, json.dumps(contact_data))
    
    def get_contact(self, phone):
        key = f"contact:{phone}"
        data = self.redis.get(key)
        return json.loads(data) if data else None
    
    def cache_conversation(self, conversation_id, messages):
        key = f"conversation:{conversation_id}"
        self.redis.setex(key, self.conversation_ttl, json.dumps(messages))
```

### Batch Operations
```python
# Batch message sending
class BatchMessageSender:
    def __init__(self, batch_size=50):
        self.batch_size = batch_size
        self.pending_messages = []
    
    def add_message(self, recipient, message):
        self.pending_messages.append({
            "to": recipient,
            "text": message,
            "timestamp": time.time()
        })
        
        if len(self.pending_messages) >= self.batch_size:
            self.send_batch()
    
    def send_batch(self):
        if not self.pending_messages:
            return
        
        # Group messages by recipient to avoid spam
        grouped = {}
        for msg in self.pending_messages:
            recipient = msg["to"]
            if recipient not in grouped:
                grouped[recipient] = []
            grouped[recipient].append(msg)
        
        # Send messages with appropriate delays
        for recipient, messages in grouped.items():
            for i, msg in enumerate(messages):
                if i > 0:
                    time.sleep(1)  # 1 second delay between messages to same recipient
                self.send_single_message(msg)
        
        self.pending_messages.clear()
```

## Links

- [WhatsApp MCP Repository](https://github.com/lharries/whatsapp-mcp)
- [WhatsApp Business API Documentation](https://developers.facebook.com/docs/whatsapp)
- [GreenAPI WhatsApp MCP](https://github.com/msaelices/whatsapp-mcp-server)
- [WhatsApp Business API Pricing](https://developers.facebook.com/docs/whatsapp/pricing)
- [WhatsApp Commerce Policy](https://www.whatsapp.com/legal/commerce-policy)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [WhatsApp MCP Community](https://github.com/lharries/whatsapp-mcp/discussions)
- [WhatsApp Business API Forum](https://developers.facebook.com/community/whatsapp-business)
- [WhatsApp MCP Examples](https://github.com/lharries/whatsapp-mcp/tree/main/examples)
- [WhatsApp Business Best Practices](https://business.whatsapp.com/resources)
- [MCP Discord](https://discord.gg/mcp)
- [WhatsApp Developer Support](https://developers.facebook.com/support/whatsapp-business-api)

