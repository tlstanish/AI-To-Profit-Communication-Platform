Purpose
The Rewrite Engine Prompt transforms any original_message into a clear, professional, on‑brand, and channel‑appropriate message using the business’s:

VoiceDNA (voice_profile)

Communication Profile (communication_profile)

Channel Rules (channel_rules)

Rewrite Preferences (rewrite_preferences)

It ensures:

Tone consistency

Style consistency

Safety compliance

Channel formatting

Removal of risky or unclear language

Use of approved brand phrases

Avoidance of banned phrases

This prompt is used by both Offer 1 (Customer OS) and Offer 2 (Operations OS).

Inputs
The prompt receives a JSON object with the following fields:

original_message
The raw message written by a human or customer.

voice_profile
Defines the business’s VoiceDNA, including:

tone_keywords

style_keywords

formality_level

empathy_level

brand_phrases

do_not_say_list

greeting_style

signoff_style

communication_profile
Defines communication rules and safety constraints, including:

sms_max_length

sms_style_notes

email_style_notes

webchat_style_notes

phone_script_style_notes

safety_rules

compliance_notes

escalation_triggers

channel_rules
Defines formatting rules for each channel, including:

sms_formatting_rules

email_formatting_rules

webchat_formatting_rules

phone_script_formatting_rules

grasshopper_routing_rules

grasshopper_sms_rules

rewrite_preferences
Defines how the rewrite should be shaped, including:

rewrite_tone

rewrite_clarity_rules

rewrite_structure_rules

rewrite_safety_rules

Outputs
The model must return only this JSON object:

json
{
  "rewritten_message": "string",
  "safety_flags": ["string"]
}
rewritten_message
The final, ready‑to‑send message rewritten using all rules and preferences.

safety_flags
An array of warnings or notes about:

risky language

compliance issues

escalation triggers

unsafe claims

vague or misleading statements

If no issues exist, return an empty array.

Example
Example Input
json
{
  "original_message": "Yeah we can probably do it for like 200 bucks, not sure though.",
  "voice_profile": {
    "tone_keywords": ["friendly", "professional"],
    "style_keywords": ["clear", "simple"],
    "formality_level": "neutral",
    "empathy_level": "medium",
    "brand_phrases": ["We’d be happy to help."],
    "do_not_say_list": ["not sure", "I guess"],
    "greeting_style": "Hi {name},",
    "signoff_style": "Thanks,"
  },
  "communication_profile": {
    "sms_max_length": 240,
    "sms_style_notes": "Short, clear, no jargon.",
    "email_style_notes": "Friendly, slightly more detailed.",
    "webchat_style_notes": "Conversational, quick.",
    "phone_script_style_notes": "Spoken, natural.",
    "safety_rules": ["Do not give exact quotes if unsure.", "Avoid vague pricing."],
    "compliance_notes": "",
    "escalation_triggers": ["refund", "angry", "lawyer"]
  },
  "channel_rules": {
    "sms_formatting_rules": ["Keep under 240 characters."],
    "email_formatting_rules": ["Use greeting and signoff."],
    "webchat_formatting_rules": [],
    "phone_script_formatting_rules": [],
    "grasshopper_routing_rules": [],
    "grasshopper_sms_rules": []
  },
  "rewrite_preferences": {
    "rewrite_tone": "friendly and confident",
    "rewrite_clarity_rules": ["Be specific where possible.", "Avoid vague language."],
    "rewrite_structure_rules": ["One or two short sentences."],
    "rewrite_safety_rules": ["Avoid firm quotes if not confirmed."]
  }
}
Example Output
json
{
  "rewritten_message": "We’d be happy to help. Our pricing typically starts around $200, and I can give you a precise quote once I know a few more details.",
  "safety_flags": [
    "Original message contained vague pricing and uncertainty; rewritten to be clearer and safer."
  ]
}
