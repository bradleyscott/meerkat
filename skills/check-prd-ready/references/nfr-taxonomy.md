# NFR Taxonomy

Non-functional requirements (NFRs) describe the quality attributes a feature must have — not what it does, but how well it does it. These are business-level requirements; engineering decides how to meet them.

Evaluate only the categories relevant to the feature being reviewed. Skip inapplicable categories without justification.

---

## Performance

Does the feature need to meet specific response time, throughput, or load requirements?

**Examples of business-level requirements:**
- "Search results must appear within 2 seconds under typical load"
- "The feature must support [X] concurrent users without degradation"
- "Bulk operations must complete within [Y] minutes for typical data volumes"
- "The feature must not meaningfully degrade the performance of adjacent features"

**When it applies:** Features that are user-facing with a perceived speed component, batch operations, or features expected to handle high volumes.

---

## Security

Are there specific security requirements beyond the platform's baseline?

**Examples of business-level requirements:**
- "Only users with [role] permission may access [data/action]"
- "All [type of data] must be encrypted at rest"
- "Audit logs must record who performed [action] and when"
- "Authentication must be required before accessing [feature]"

**When it applies:** Features that handle sensitive data, modify permissions, expose new API endpoints, or have compliance implications.

---

## Privacy and Data Handling

How should personal or sensitive data be handled, stored, and retained?

**Examples of business-level requirements:**
- "Personal data collected must be limited to what is necessary for [purpose]"
- "Users must be able to request deletion of their [data type]"
- "Data must not be retained beyond [period]"
- "The feature must comply with [regulation, e.g., GDPR, HIPAA, CCPA] in the regions it operates"
- "Users must be informed that [data] is being collected"

**When it applies:** Features that collect, process, store, or transmit personal or sensitive data.

---

## Accessibility

Does the feature need to be usable by people with disabilities?

**Examples of business-level requirements:**
- "The feature must be operable via keyboard without a mouse"
- "All images and icons must have descriptive text alternatives"
- "The feature must meet [WCAG 2.1 AA / Section 508 / EN 301 549] standards"
- "Colour alone must not be used to convey meaning"

**When it applies:** Any user-facing feature, particularly those used by customers who may have legal accessibility requirements.

---

## Scalability

Does the feature need to handle growth in users, data volume, or usage patterns?

**Examples of business-level requirements:**
- "The feature must support [X]× current data volume without architectural changes"
- "The feature must remain functional as the user base grows from [current] to [target]"
- "The feature must not require re-engineering to support [future use case]"

**When it applies:** Features that store data expected to grow significantly, or features likely to be extended with higher-volume use cases.

---

## Reliability and Availability

What uptime or reliability expectations apply to this feature?

**Examples of business-level requirements:**
- "The feature must be available [99.9%] of the time during business hours"
- "Failures must not result in data loss"
- "If [dependency] is unavailable, the feature must degrade gracefully rather than failing completely"
- "Recovery from an outage must complete within [time period]"

**When it applies:** Features on critical user paths, features with SLA obligations, or features where failure has significant customer impact.

---

## Internationalisation

Does the feature need to work across different languages, locales, or regions?

**Examples of business-level requirements:**
- "The feature must support [languages]"
- "Dates, times, and numbers must display in the user's local format"
- "The feature must support right-to-left text rendering"
- "Currency values must be displayed in the appropriate regional format"

**When it applies:** Features available in multiple countries or language markets, or features with date/time/number display.
