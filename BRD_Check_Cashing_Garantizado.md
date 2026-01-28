# Business Requirements Document (BRD)
## Check Cashing Garantizado - Maxi

**Document Version:** 1.0  
**Date:** January 28, 2026  
**Project:** Guaranteed Check Cashing System  
**Prepared By:** Development Team  
**Based On:** Requirements from discovery calls (June 30 - July 8, 2025) and design documentation

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Project Overview](#2-project-overview)
3. [Business Objectives](#3-business-objectives)
4. [Stakeholders](#4-stakeholders)
5. [Scope](#5-scope)
6. [Functional Requirements](#6-functional-requirements)
7. [Non-Functional Requirements](#7-non-functional-requirements)
8. [System Architecture](#8-system-architecture)
9. [Integration Points](#9-integration-points)
10. [User Interface Requirements](#10-user-interface-requirements)
11. [Business Rules](#11-business-rules)
12. [Workflows and Process Flows](#12-workflows-and-process-flows)
13. [Data Requirements](#13-data-requirements)
14. [Assumptions and Constraints](#14-assumptions-and-constraints)
15. [Success Criteria](#15-success-criteria)
16. [Outstanding Items](#16-outstanding-items)
17. [Appendices](#17-appendices)

---

## 1. Executive Summary

This Business Requirements Document (BRD) outlines the requirements for implementing a **Guaranteed Check Cashing System** (Check Cashing Garantizado) at Maxi. Unlike the traditional check processing service where agents bear the responsibility for fraudulent checks, this new system transfers 100% of the check liability to Maxi, requiring robust fraud detection, compliance verification, and collections management capabilities.

The system will integrate automated check validation through **Valid Systems**, manual compliance review processes, real-time OFAC/AML screening, and a comprehensive collections workflow for bounced checks. The solution spans both front-end agent operations (Hermes 2.0) and back-office processes (Cronos) to ensure secure, compliant, and efficient check cashing services.

**Key Differentiators:**
- Maxi assumes 100% liability for guaranteed checks
- Automated validation with manual override capabilities
- Integrated compliance screening (OFAC, KYC, BSA)
- Structured collections process with dedicated team (50+ personnel)
- Multi-tiered hold management and escalation workflows

---

## 2. Project Overview

### 2.1 Background

Maxi currently offers check processing services where agents assume the risk of fraudulent checks, leading to collection challenges and agent debt. The guaranteed check cashing service shifts this liability to Maxi, positioning the company to compete with services like Barry that offer similar guaranteed check cashing.

### 2.2 Business Context

The check cashing industry requires:
- Strong fraud detection mechanisms
- Regulatory compliance (OFAC, BSA, AML)
- Robust collections infrastructure
- Fast customer service (target: under 5 minutes per transaction)
- Multi-state compliance (42 states with varying receipt requirements)

### 2.3 Project Goals

1. Launch a secure guaranteed check cashing service
2. Minimize fraud losses through automated and manual validation
3. Ensure regulatory compliance across all transactions
4. Establish efficient collections processes for bounced checks
5. Provide excellent customer experience with rapid service

---

## 3. Business Objectives

### 3.1 Primary Objectives

1. **Risk Mitigation**: Reduce fraud losses to acceptable levels through multi-layered validation
2. **Revenue Generation**: Create new revenue stream from check cashing fees (percentage-based)
3. **Customer Expansion**: Serve both existing and new Maxi customers
4. **Regulatory Compliance**: Maintain 100% compliance with AML, KYC, OFAC, and BSA requirements
5. **Operational Efficiency**: Process checks within 5-minute target timeframe
6. **Collections Recovery**: Achieve target recovery rates on bounced checks

### 3.2 Success Metrics

- **Fraud Rate**: Target < 2% of total check volume
- **Recovery Rate**: Target > 70% on bounced checks
- **Processing Time**: Average < 5 minutes per transaction
- **Compliance Score**: 100% regulatory adherence
- **Customer Satisfaction**: Target > 85% positive feedback
- **Agent Commission**: Percentage-based compensation on successful transactions

---

## 4. Stakeholders

### 4.1 Internal Stakeholders

| Department | Role | Responsibilities |
|------------|------|------------------|
| **Front-End Agents/Tellers** | Transaction Execution | Check scanning, KYC data entry, customer service |
| **Compliance Team (Back Office)** | Risk Management | Manual validation, hold review, OFAC/KYC verification |
| **Collections Department** | Debt Recovery | Contact with debtors, payment tracking, case management (50 personnel) |
| **BSA Analysts** | Regulatory Compliance | SAR/CTR generation, alert review, compliance reporting |
| **KYC Analysts** | Customer Verification | Customer identity validation, document review |
| **Fraud Prevention Team** | Pattern Analysis | Fraud investigation, pattern detection, deny list management |
| **Agent Oversight** | Quality Assurance | Agent performance monitoring, training, corrective actions |
| **Treasury/Finance** | Financial Operations | Payment verification, reconciliation, fund management |
| **IT/Development Team** | System Implementation | Development, integration, testing, deployment |
| **Legal/Compliance** | Regulatory Oversight | Policy definition, legal compliance, documentation |
| **Product Management** | Business Ownership | Requirements definition, stakeholder coordination |

### 4.2 External Stakeholders

- **Valid Systems**: Check validation service provider
- **Banks**: Check deposit and clearing partners
- **Customers**: Check cashing service recipients
- **Check Issuers**: Entities/individuals writing checks
- **Regulatory Bodies**: Financial regulators, state authorities

---

## 5. Scope

### 5.1 In Scope

**Front-End Operations (Hermes 2.0):**
- Check scanning with OCR capture (Mitek integration)
- Customer search and creation with full KYC
- Phone verification via 6-digit SMS code
- Issuer search and creation
- Bank validation and routing number verification
- Fee calculation (percentage-based)
- Valid Systems integration for automated check validation
- Manual review flagging capability
- Receipt generation and printing
- Agent reporting and commission tracking

**Back-Office Operations (Cronos):**
- Multi-category hold management (OFAC, KYC, Edit, Duplicate, Validation)
- Manual validation queue for compliance analysts
- Collections workflow with case assignment and tracking
- Payment confirmation and reconciliation
- Deny list management (customer and issuer blacklisting)
- Alert generation (SAR, CTR, pattern-based)
- Supervisor escalation workflows
- KPI dashboard and reporting
- Communication module (SMS, Email)

**Compliance & Security:**
- OFAC screening integration (Nemesis)
- AML/BSA compliance workflows
- Audit trail for all transactions and decisions
- Fraud pattern detection
- Multi-level approval processes

**Collections Management:**
- Bounced check registration
- Priority-based case assignment (amount + age)
- Contact management (phone, SMS, email)
- Payment tracking and verification
- Escalation to legal/fraud teams
- Recovery reporting and KPIs

### 5.2 Out of Scope (MVP)

- Offline check processing (suspended module)
- Letter generation for collections (Phase 2)
- Automated rules builder UI (Phase 2)
- Mobile customer app
- Integration with additional validation providers beyond Valid Systems
- International check processing
- Check deposit via mobile capture
- Payroll check processing (specialized rules deferred)

### 5.3 Future Enhancements

- Advanced rules builder for business logic configuration
- Letter generation and mailing automation
- Multi-language support
- Enhanced reporting and analytics
- Integration with additional fraud detection services
- Mobile agent application
- Customer self-service portal

---

## 6. Functional Requirements

### 6.1 Front-End Module (Hermes 2.0)

#### 6.1.1 Check Scanning and OCR

**Requirement ID:** FR-FE-001  
**Description:** System shall capture check information via scanner and OCR technology

**Acceptance Criteria:**
- Scan check and extract routing number, account number, check number, amount, date
- Display captured information for agent verification
- Allow manual correction of OCR errors
- Support standard check formats
- Handle poor quality scans with error messaging

**Priority:** CRITICAL

---

#### 6.1.2 Customer Search and Creation

**Requirement ID:** FR-FE-002  
**Description:** System shall enable customer search and new customer creation with full KYC

**Acceptance Criteria:**
- Search existing customers by name, phone, or customer ID
- Display search results with customer details
- Create new customer if not found
- Capture required KYC fields:
  - Full name (first name, first surname, second surname)
  - Complete address (exterior number, interior number, postal code, city, state)
  - Date of birth
  - Occupation and sub-occupation
  - Country of birth
  - Primary mobile phone (required)
  - Secondary mobile phone (optional)
  - Email address
  - Tax ID type and number
  - Customer ID (country, ID type, issuing state, ID number, expiration date)
  - ID photos (front and back)
  - Customer photo
- Validate all required fields before submission
- Display summary for agent review before acceptance

**Priority:** CRITICAL

---

#### 6.1.3 Phone Verification

**Requirement ID:** FR-FE-003  
**Description:** System shall verify customer phone number via SMS code

**Acceptance Criteria:**
- Send 6-digit verification code via SMS to provided phone number
- Display code entry screen
- Validate entered code against sent code
- Allow code resend (with time limits to prevent abuse)
- Timeout after 3 failed attempts
- Block customer creation if verification fails

**Priority:** CRITICAL

---

#### 6.1.4 Issuer Management

**Requirement ID:** FR-FE-004  
**Description:** System shall manage check issuer information

**Acceptance Criteria:**
- OCR captures issuer name from check
- Search for existing issuer in database
- Display issuer search results
- Allow selection of existing issuer
- Create new issuer if not found
- Capture issuer details:
  - Issuer name
  - Bank selection from dropdown
  - Account validation
- Display issuer summary for confirmation
- Associate issuer samples with issuer (not just bank)

**Priority:** CRITICAL

---

#### 6.1.5 Bank Validation

**Requirement ID:** FR-FE-005  
**Description:** System shall validate bank information against check details

**Acceptance Criteria:**
- Extract routing number from check OCR
- Match routing number to bank in database
- Display bank dropdown for selection
- Perform side-by-side comparison of check image vs. bank sample
- Flag mismatches for manual review
- Update bank catalog monthly
- If bank changed manually, send to "Edit Hold"

**Priority:** CRITICAL

---

#### 6.1.6 Check Validation via Valid Systems

**Requirement ID:** FR-FE-006  
**Description:** System shall integrate with Valid Systems for automated check validation

**Acceptance Criteria:**
- Send check details to Valid Systems API
- Receive validation response (Accept, Review, Decline)
- Display validation result to agent
- Handle three outcomes:
  - **Accepted**: Proceed to payment
  - **Under Review**: Hold check, notify customer of delay
  - **Declined**: Reject transaction, provide reason
- Support validation timeout (up to 5 minutes)
- Display loader with option to wait or cancel
- If Valid Systems unavailable, suspend module with manual override option

**Priority:** CRITICAL

---

#### 6.1.7 Manual Review Flagging

**Requirement ID:** FR-FE-007  
**Description:** System shall allow agents to flag suspicious transactions for manual review

**Acceptance Criteria:**
- Provide checkbox for "Requires Manual Validation"
- Allow agent to add notes explaining suspicion
- Send flagged checks to Validation Hold queue
- Log agent observation (e.g., nervous customer, suspicious behavior)
- Continue transaction flow but mark for back-office review before payment release

**Priority:** HIGH

---

#### 6.1.8 Fee Calculation

**Requirement ID:** FR-FE-008  
**Description:** System shall calculate fees as percentage of check amount

**Acceptance Criteria:**
- Calculate check cashing fee as configurable percentage
- Display fee breakdown:
  - Check amount
  - Check cashing fee
  - Agent commission
  - Net credit to customer
  - Total transaction amount
- Support fee override (with supervisor approval)
- Log all fee calculations for audit

**Priority:** CRITICAL

---

#### 6.1.9 Receipt Generation and Printing

**Requirement ID:** FR-FE-009  
**Description:** System shall generate and print receipts compliant with multi-state regulations

**Acceptance Criteria:**
- Generate receipt with all required fields per state regulations (42 states)
- Display receipt preview to agent
- Support multiple print options:
  - Ticket printer
  - Laser printer
  - Email receipt
- Include receipt elements:
  - Transaction ID/folio
  - Date and time
  - Customer name
  - Check amount
  - Fee amount
  - Net amount
  - Agent ID and location
  - Legal disclosures per state
- Reprint capability with original transaction lookup

**Priority:** HIGH

---

#### 6.1.10 Transaction Status Display

**Requirement ID:** FR-FE-010  
**Description:** System shall display real-time transaction status

**Acceptance Criteria:**
- Show status indicators:
  - Processing (during validation)
  - Accepted (ready for payment)
  - Under Review (held for manual validation)
  - Declined (rejected)
- Update status in real-time as validation completes
- Display clear next steps for each status
- Allow agent to explain status to customer

**Priority:** HIGH

---

#### 6.1.11 Agent Reporting

**Requirement ID:** FR-FE-011  
**Description:** System shall provide agent-level transaction reporting

**Acceptance Criteria:**
- Filter transactions by date range
- Search by check number or transaction ID
- Display agent's transactions with:
  - Transaction date/time
  - Customer name
  - Check amount
  - Fee amount
  - Commission earned
  - Transaction status
- Calculate total commissions for period
- Export reports to PDF/Excel

**Priority:** MEDIUM

---

### 6.2 Back-Office Module (Cronos)

#### 6.2.1 Hold Management Dashboard

**Requirement ID:** FR-BO-001  
**Description:** System shall provide categorized hold queues for different hold types

**Acceptance Criteria:**
- Display separate queues for:
  - **Validation Hold**: Flagged by system or agent as risky
  - **OFAC Hold**: Name match on OFAC watchlist
  - **KYC Hold**: Missing or suspicious customer documentation
  - **Edit Hold**: Manual changes made by agent
  - **Duplicate Hold**: Potential duplicate check detected
- Show count of items in each queue
- Prioritize by hold age and risk level
- Support filtering and sorting
- Color-code by urgency

**Priority:** CRITICAL

---

#### 6.2.2 Manual Validation Queue

**Requirement ID:** FR-BO-002  
**Description:** System shall enable compliance analysts to review and resolve holds

**Acceptance Criteria:**
- Display full check details:
  - Customer information (name, ID, photo)
  - Issuer information
  - Check image (front and back if available)
  - Bank sample comparison
  - Transaction history
  - Hold reason and notes
- Provide decision options:
  - **Accept**: Release check for payment
  - **Decline**: Reject check with reason selection
  - **Escalate**: Send to fraud investigation team
  - **Request More Info**: Return to agent for additional details
- Log all analyst actions with timestamp and user ID
- Support manual bank verification (phone call to bank)
- Allow addition to Deny List during review

**Priority:** CRITICAL

---

#### 6.2.3 Collections Management System

**Requirement ID:** FR-BO-003  
**Description:** System shall manage bounced check collections workflow

**Acceptance Criteria:**
- Register bounced checks from bank returns
- Prioritize cases by:
  - Check amount (higher amounts prioritized)
  - Age (older cases prioritized)
- Display collections queue with:
  - Customer/Issuer name
  - Check amount
  - Bounce date
  - Days outstanding
  - Contact history
  - Case status
- Support case assignment:
  - Supervisor assigns to specific collectors
  - Automatic assignment based on workload
  - Manual reassignment capability
- Track contact attempts:
  - Phone calls (date, time, outcome)
  - SMS sent
  - Emails sent
  - Customer responses
- Categorize case outcomes:
  - Payment promised (with promised date)
  - No response
  - Not located
  - Refused to pay
  - Not the account holder
  - Does not recognize charge
- Support payment registration and confirmation
- Escalate to legal/fraud as needed

**Priority:** CRITICAL

---

#### 6.2.4 Payment Confirmation and Reconciliation

**Requirement ID:** FR-BO-004  
**Description:** System shall verify and reconcile customer payments

**Acceptance Criteria:**
- Allow collectors to register payment received
- Capture payment details:
  - Payment amount
  - Payment date
  - Payment method (bank deposit, cash, etc.)
  - Bank confirmation number
- Upload supporting documentation
- Flag discrepancies (partial payments, overpayments)
- Integrate with Treasury for bank reconciliation
- Generate reconciliation reports
- Mark case as closed upon full payment and confirmation

**Priority:** HIGH

---

#### 6.2.5 Deny List Management

**Requirement ID:** FR-BO-005  
**Description:** System shall maintain blacklist for customers and issuers

**Acceptance Criteria:**
- Add customers to Deny List with reason:
  - Fraud confirmed
  - Repeat offender
  - Legal restrictions
- Add issuers to Deny List with reason
- Display Deny List with search and filter
- Block transactions from denied parties
- Support removal from Deny List (with supervisor approval)
- Log all additions/removals with audit trail
- Alert agents in real-time if customer/issuer on Deny List

**Priority:** CRITICAL

---

#### 6.2.6 Alert Generation and Management

**Requirement ID:** FR-BO-006  
**Description:** System shall generate compliance alerts for suspicious patterns

**Acceptance Criteria:**
- Auto-generate alerts based on:
  - Multiple checks from same postal code
  - Name similarities (potential identity fraud)
  - Same issuer with multiple beneficiaries
  - High-volume activity from new customers
  - Pattern matching (time, location, amount)
- Route alerts to appropriate teams:
  - OFAC matches → BSA Analysts
  - Fraud patterns → Fraud Prevention
  - KYC issues → KYC Analysts
- Display alert dashboard with:
  - Alert type
  - Risk level (Critical, High, Medium, Low)
  - Status (New, Under Review, Resolved)
  - Assigned analyst
- Generate SAR (Suspicious Activity Report) when warranted
- Generate CTR (Currency Transaction Report) for large amounts
- Track alert resolution status

**Priority:** HIGH

---

#### 6.2.7 Exception Rules Configuration

**Requirement ID:** FR-BO-007  
**Description:** System shall support business rules configuration for overrides

**Acceptance Criteria:**
- Define exception rules for:
  - Check amounts (thresholds for auto-approval)
  - Issuer types (corporate vs. personal)
  - Customer risk profiles
  - Geographic restrictions
- Support supervisor approval for rule overrides
- Log all rule executions and overrides
- Provide rule effectiveness analytics
- Phase 2: Visual rules builder UI

**Priority:** MEDIUM (Phase 2 for full UI)

---

#### 6.2.8 KPI Dashboard

**Requirement ID:** FR-BO-008  
**Description:** System shall provide performance metrics and KPIs

**Acceptance Criteria:**
- Display collections KPIs:
  - Recovery rate (%)
  - Average recovery time (days)
  - Daily contacts made
  - Contact effectiveness rate
  - SLA compliance
  - Cases by status
- Display compliance KPIs:
  - Hold resolution time
  - Fraud detection rate
  - Escalation rates
  - Analyst productivity
- Display operational KPIs:
  - Transaction volume
  - Average processing time
  - Decline rate
  - Agent performance
- Support date range filtering
- Export reports to Excel/PDF

**Priority:** HIGH

---

#### 6.2.9 Communication Module

**Requirement ID:** FR-BO-009  
**Description:** System shall support multi-channel customer communication

**Acceptance Criteria:**
- Send SMS notifications:
  - Phone verification codes
  - Payment reminders
  - Case updates
- Send email notifications:
  - Transaction receipts
  - Payment confirmations
  - Collections correspondence
- Track communication history
- Support template management for standardized messaging
- Log all communications for audit
- Phase 2: Letter generation and mailing

**Priority:** HIGH

---

### 6.3 Compliance and Security Requirements

#### 6.3.1 OFAC Screening

**Requirement ID:** FR-CS-001  
**Description:** System shall perform real-time OFAC screening via Nemesis

**Acceptance Criteria:**
- Screen customer names against OFAC watchlist
- Screen issuer names against OFAC watchlist
- Perform screening before transaction approval
- Flag exact and fuzzy matches
- Hold transactions with matches for manual review
- Notify BSA Analysts immediately
- Maintain screening logs for regulatory audit

**Priority:** CRITICAL

---

#### 6.3.2 AML/BSA Compliance

**Requirement ID:** FR-CS-002  
**Description:** System shall enforce AML and BSA compliance requirements

**Acceptance Criteria:**
- Capture all required KYC data
- Validate customer identity documents
- Generate SARs for suspicious activity
- Generate CTRs for qualifying transactions
- Maintain transaction records per regulatory retention policies
- Support compliance audits with searchable logs
- Integrate with Nemesis for rule execution

**Priority:** CRITICAL

---

#### 6.3.3 Audit Trail

**Requirement ID:** FR-CS-003  
**Description:** System shall maintain comprehensive audit trail

**Acceptance Criteria:**
- Log all user actions with:
  - User ID
  - Timestamp
  - Action performed
  - Data changed (before/after values)
  - IP address
  - Session ID
- Store logs in tamper-proof format
- Retain logs per regulatory requirements
- Provide audit search and report capabilities
- Support export for regulatory review

**Priority:** CRITICAL

---

### 6.4 Integration Requirements

#### 6.4.1 Valid Systems Integration

**Requirement ID:** FR-INT-001  
**Description:** System shall integrate with Valid Systems for check validation

**Acceptance Criteria:**
- Real-time API integration
- Send check data (routing, account, amount, etc.)
- Receive validation score (0-1000 scale)
- Receive decision (Accept/Review/Decline)
- Handle API timeouts gracefully
- Implement circuit breaker for system unavailability
- Log all API transactions

**Priority:** CRITICAL

---

#### 6.4.2 Bank Integration (X9 Format)

**Requirement ID:** FR-INT-002  
**Description:** System shall submit checks to banks via X9 file format

**Acceptance Criteria:**
- Generate X9 formatted files for check deposit
- Include check images and MICR data
- Batch submissions according to bank schedules
- Receive bank confirmation files
- Process return files for bounced checks
- Handle bank-specific formatting requirements

**Priority:** CRITICAL

---

#### 6.4.3 Nemesis Integration

**Requirement ID:** FR-INT-003  
**Description:** System shall integrate with Nemesis for compliance screening

**Acceptance Criteria:**
- Real-time OFAC screening
- AML rule execution
- BSA compliance checks
- Receive screening results
- Handle hold recommendations
- Log all screening activities

**Priority:** CRITICAL

---

## 7. Non-Functional Requirements

### 7.1 Performance

**Requirement ID:** NFR-PERF-001  
**Description:** System shall meet performance benchmarks

**Acceptance Criteria:**
- Transaction processing time: < 5 minutes average
- Valid Systems API response: < 30 seconds
- OFAC screening: < 5 seconds
- System uptime: 99.5% during business hours
- Support concurrent transactions: 100+ simultaneously
- Database query response: < 2 seconds for searches

**Priority:** HIGH

---

### 7.2 Scalability

**Requirement ID:** NFR-SCALE-001  
**Description:** System shall scale to support growing transaction volume

**Acceptance Criteria:**
- Support 10,000+ transactions per day
- Handle 50+ concurrent back-office users
- Database capacity for 5 years of transaction history
- Cloud infrastructure for elastic scaling

**Priority:** MEDIUM

---

### 7.3 Availability

**Requirement ID:** NFR-AVAIL-001  
**Description:** System shall maintain high availability

**Acceptance Criteria:**
- Target uptime: 99.5% during business hours (6am-10pm)
- Planned maintenance windows outside business hours
- Redundant infrastructure for critical components
- Disaster recovery capability (RPO: 1 hour, RTO: 4 hours)

**Priority:** HIGH

---

### 7.4 Security

**Requirement ID:** NFR-SEC-001  
**Description:** System shall implement robust security measures

**Acceptance Criteria:**
- Encrypt data in transit (TLS 1.2+)
- Encrypt sensitive data at rest
- Role-based access control (RBAC)
- Multi-factor authentication for back-office users
- Regular security vulnerability scanning
- PII data protection per GDPR/CCPA standards
- Secure credential management (no hardcoded secrets)

**Priority:** CRITICAL

---

### 7.5 Usability

**Requirement ID:** NFR-USE-001  
**Description:** System shall provide intuitive user experience

**Acceptance Criteria:**
- Minimal clicks to complete transaction (< 10 clicks)
- Clear error messaging with resolution guidance
- Responsive UI (load times < 3 seconds)
- Support for high-resolution screens
- Keyboard shortcuts for power users
- Training materials and online help

**Priority:** MEDIUM

---

### 7.6 Compliance

**Requirement ID:** NFR-COMP-001  
**Description:** System shall maintain regulatory compliance

**Acceptance Criteria:**
- PCI DSS compliance for payment data
- SOC 2 Type II compliance
- AML/BSA regulatory compliance
- Multi-state check cashing regulations (42 states)
- Data retention policies per legal requirements
- Regular compliance audits

**Priority:** CRITICAL

---

## 8. System Architecture

### 8.1 Architecture Overview

The Check Cashing Garantizado system follows a multi-tier architecture:

**Presentation Layer:**
- **Hermes 2.0**: Agent-facing web application
- **Cronos**: Back-office web application

**Application Layer:**
- Business logic tier
- API gateway
- Authentication/authorization services

**Integration Layer:**
- Valid Systems adapter
- Nemesis adapter
- Bank integration services
- SMS/Email gateway

**Data Layer:**
- Transactional database (customer, transactions, checks)
- Document storage (check images, ID photos)
- Audit log database
- Configuration database

**External Systems:**
- Valid Systems (check validation)
- Nemesis (compliance screening)
- Banks (check processing)
- SMS/Email providers

---

### 8.2 Technology Stack (To Be Determined)

- **Frontend**: Modern web framework (React, Angular, or Vue.js)
- **Backend**: Enterprise application framework
- **Database**: Relational database (PostgreSQL, Oracle, or SQL Server)
- **Document Storage**: Object storage or file system
- **API**: RESTful APIs with JSON
- **Security**: OAuth 2.0, JWT tokens
- **Monitoring**: Application performance monitoring (APM)

---

## 9. Integration Points

| System | Purpose | Direction | Protocol | Criticality |
|--------|---------|-----------|----------|-------------|
| **Valid Systems** | Check validation scoring | Real-time API call | REST/SOAP | CRITICAL |
| **Nemesis** | OFAC/AML screening | Real-time API call | REST/SOAP | CRITICAL |
| **Banks** | Check deposit submission | Batch file transfer | X9 format (SFTP) | CRITICAL |
| **SMS Gateway** | Phone verification, notifications | Outbound API | REST | HIGH |
| **Email System** | Receipts, collections correspondence | Outbound API | SMTP/REST | HIGH |
| **Oracle Financials / BlackLine** | Payment reconciliation | Batch integration | File/API | HIGH |
| **Hermes 2.0** | Agent transaction processing | Internal integration | Database | CRITICAL |
| **Cronos** | Back-office workflows | Internal integration | Database | CRITICAL |

---

## 10. User Interface Requirements

### 10.1 Hermes 2.0 Screens

Based on the screen diagrams and process flows:

1. **Check Scanning Screen**
   - Check image display
   - OCR data capture fields
   - Manual correction capability

2. **Customer Search/Creation Screen**
   - Search bar with filters
   - Search results grid
   - New customer form with KYC fields

3. **Phone Verification Screen**
   - 6-digit code entry
   - Resend code button
   - Timer display

4. **Customer Photo Capture Screen**
   - Live camera feed
   - ID front/back photo capture
   - Photo preview and retake

5. **Issuer Search/Creation Screen**
   - Issuer search
   - New issuer form
   - Bank selection dropdown

6. **Check Validation Screen**
   - Side-by-side check comparison
   - Field-by-field validation
   - Manual override options

7. **Validation Result Screen**
   - Status indicator (Accepted/Review/Declined)
   - Next steps guidance
   - Agent dispute option

8. **Fee Summary Screen**
   - Check amount
   - Fee breakdown
   - Net to customer
   - Confirm button

9. **Receipt Screen**
   - Receipt preview
   - Print/email options
   - Printer selection

10. **Agent Reports Screen**
    - Date range filters
    - Transaction list
    - Commission summary

---

### 10.2 Cronos Screens

1. **Holds Dashboard**
   - Queue summary cards (counts by type)
   - Quick navigation to queues
   - Priority indicators

2. **Validation Queue**
   - Filterable/sortable grid
   - Check details panel
   - Decision buttons

3. **Check Detail Screen**
   - Full customer info
   - Check images
   - Transaction history
   - Hold reason and notes

4. **Collections Dashboard**
   - KPI cards
   - Case list
   - Assignment interface

5. **Collections Case Detail**
   - Customer contact info
   - Payment history
   - Contact log
   - Payment registration form

6. **Deny List Management**
   - Search and filter
   - Add/remove controls
   - Reason documentation

7. **Alert Management**
   - Alert queue
   - Risk categorization
   - Assignment and resolution tracking

8. **KPI Dashboard**
   - Visual charts (bar, line, pie)
   - Metric cards
   - Date range selector
   - Export buttons

9. **Rules Configuration** (Phase 2)
   - Rule builder interface
   - Parameter settings
   - Testing and validation

---

## 11. Business Rules

### 11.1 Validation Rules

1. **Auto-Approval Thresholds**: Checks below configurable amount with clean validation may auto-approve
2. **Behavioral Scoring**: Valid Systems score 0-1000, threshold configurable (e.g., >700 = approve, 400-700 = review, <400 = decline)
3. **OFAC Match**: Any OFAC match results in immediate hold
4. **Deny List**: Customer or issuer on Deny List results in automatic decline
5. **Duplicate Detection**: Same check number + routing number + account number within 30 days triggers duplicate hold
6. **Manual Edit**: Any field edited by agent triggers Edit Hold for compliance review

---

### 11.2 Collections Rules

1. **Prioritization**: Cases prioritized by formula: (Amount × Weight1) + (Days Outstanding × Weight2)
2. **Contact Sequence**: Phone → SMS → Email (with configurable intervals)
3. **Escalation**: Cases unresolved after 30 days escalate to legal
4. **Payment Confirmation**: All payments require bank confirmation or transaction proof
5. **Partial Payments**: Accepted with remaining balance tracked

---

### 11.3 Fee Calculation

1. **Fee Structure**: Percentage-based fee on check amount (configurable per state/region)
2. **Agent Commission**: Percentage of fee earned on successful transactions
3. **Fee Caps**: Maximum fee limits per state regulations
4. **Refunds**: If check bounces, fees may be refunded per policy

---

## 12. Workflows and Process Flows

### 12.1 Primary Check Cashing Flow

```
1. Agent scans check → OCR captures data
2. Agent searches for customer
   ├─ Found: Select customer → Go to step 3
   └─ Not found: Create new customer
      ├─ Capture KYC data
      ├─ Verify phone with 6-digit SMS code
      ├─ Capture ID photos
      ├─ Capture customer photo
      └─ Review summary → Accept → Go to step 3
3. Agent searches for issuer
   ├─ Found: Select issuer → Go to step 4
   └─ Not found: Create new issuer → Go to step 4
4. Validate check information
   ├─ Review OCR data
   ├─ Compare with bank sample
   ├─ Make manual corrections if needed
   └─ Flag for manual review if suspicious
5. Submit to Valid Systems
   ├─ Display loader (up to 5 min wait)
   └─ Receive result:
      ├─ Accepted: Go to step 6
      ├─ Review: Hold check, notify customer
      └─ Declined: Reject, return check to customer
6. Display fee summary
   └─ Agent confirms
7. Generate receipt
   ├─ Print if requested
   └─ Complete transaction
```

---

### 12.2 Hold Review Flow (Back Office)

```
1. Check enters hold queue (OFAC, KYC, Edit, Duplicate, Validation)
2. Analyst selects check from queue
3. Review check details
   ├─ Customer information
   ├─ Check images
   ├─ Transaction history
   └─ Hold reason
4. Perform validation:
   ├─ OFAC Hold: Verify against watchlist
   ├─ KYC Hold: Review documentation
   ├─ Edit Hold: Verify manual changes
   ├─ Duplicate Hold: Compare side-by-side
   └─ Validation Hold: Investigate fraud patterns, call bank if needed
5. Make decision:
   ├─ Accept: Release check → Payment proceeds
   ├─ Decline: Reject check → Notify agent and customer
   ├─ Escalate: Send to fraud investigation
   └─ Request Info: Return to agent for clarification
6. Document decision and rationale
7. Log action in audit trail
```

---

### 12.3 Collections Flow

```
1. Bank returns bounced check
2. System registers in collections queue
3. Prioritize by amount and age
4. Supervisor assigns to collector
5. Collector reviews case
   ├─ Customer history
   ├─ Check details
   └─ Previous contact attempts
6. Initiate contact:
   ├─ Phone call
   ├─ SMS if no answer
   └─ Email if unreachable
7. Log contact outcome:
   ├─ Payment promised: Schedule follow-up
   ├─ No response: Retry per schedule
   ├─ Not located: Escalate to skip tracing
   ├─ Refused to pay: Escalate to legal
   ├─ Not account holder: Investigate fraud
   └─ Does not recognize: Investigate fraud
8. If payment received:
   ├─ Register payment in system
   ├─ Upload bank confirmation
   ├─ Verify with treasury
   └─ Close case
9. If unresolved after 30 days:
   └─ Escalate to legal/fraud team
```

---

### 12.4 Compliance Alert Flow

```
1. System generates alert based on pattern detection
2. Alert routed to appropriate team:
   ├─ OFAC match → BSA Analyst
   ├─ Fraud pattern → Fraud Prevention
   └─ KYC issue → KYC Analyst
3. Analyst reviews alert
   ├─ Gather supporting data
   ├─ Analyze patterns
   └─ Assess risk level
4. Take action:
   ├─ Generate SAR if warranted
   ├─ Add to Deny List
   ├─ Escalate to supervisor
   ├─ Investigate further
   └─ Close as false positive
5. Document resolution
6. Update alert status
```

---

## 13. Data Requirements

### 13.1 Customer Data

**Required Fields:**
- Full name (first, middle, surname 1, surname 2)
- Complete address
- Date of birth
- Phone number(s)
- Email
- Occupation
- Country of birth
- Tax ID
- ID type, number, expiration, photos
- Customer photo

**Storage Requirements:**
- Encrypted storage for PII
- Shared database across Maxi products
- Retention: 7 years minimum

---

### 13.2 Transaction Data

**Required Fields:**
- Transaction ID (unique)
- Date and time
- Customer ID
- Issuer ID
- Check details (number, amount, routing, account)
- Bank ID
- Validation result
- Fee and commission
- Agent ID
- Location ID
- Status history

**Storage Requirements:**
- Immutable transaction records
- Audit trail for all changes
- Retention: 7 years minimum

---

### 13.3 Check Images

**Required Fields:**
- Front image (high resolution)
- Back image (if applicable)
- OCR extracted data

**Storage Requirements:**
- Secure document storage
- Image quality standards
- Retention: 7 years minimum

---

## 14. Assumptions and Constraints

### 14.1 Assumptions

1. Valid Systems API will be available 99% of the time
2. Bank relationships established for X9 file processing
3. SMS gateway capacity sufficient for verification codes
4. Agents will be trained on new KYC requirements
5. Collections team of 50+ personnel will be hired and trained
6. Regulatory approvals obtained for guaranteed check cashing in target states
7. Existing Hermes 2.0 and Cronos platforms can be extended for this functionality

---

### 14.2 Constraints

1. **MVP Constraint**: Offline processing not available (suspended module)
2. **Technical Constraint**: Valid Systems integration is single point of failure; suspension required if unavailable
3. **Regulatory Constraint**: Must comply with 42 state regulations for receipts and disclosures
4. **Timeline Constraint**: Project must launch within defined timeline (TBD)
5. **Budget Constraint**: Limited budget for external integrations and new hires
6. **Operational Constraint**: Agent processing time target of < 5 minutes
7. **Data Constraint**: Shared customer database means data model alignment with other products

---

### 14.3 Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| Valid Systems downtime | HIGH | Implement suspension mode; have manual override process |
| Fraud losses exceed projections | HIGH | Conservative validation thresholds initially; continuous monitoring |
| Collections recovery rate below target | MEDIUM | Hire experienced collectors; implement best practices |
| Regulatory non-compliance | CRITICAL | Engage legal/compliance early; regular audits |
| Integration delays | MEDIUM | Parallel development where possible; early integration testing |
| Agent adoption challenges | MEDIUM | Comprehensive training; user-friendly UI design |

---

## 15. Success Criteria

The project will be considered successful when:

1. **Functional Completeness**: All critical functional requirements implemented and tested
2. **Regulatory Compliance**: Pass compliance audit for all 42 states
3. **Performance Targets Met**: 
   - Average transaction time < 5 minutes
   - System uptime > 99.5%
4. **Fraud Rate Acceptable**: Fraud losses < 2% of transaction volume
5. **Collections Performance**: Recovery rate > 70%
6. **User Acceptance**: 
   - Agent satisfaction > 80%
   - Back-office user satisfaction > 80%
7. **Integration Success**: All external integrations operational
8. **Training Complete**: All users trained and certified

---

## 16. Outstanding Items

The following items require further clarification or decision:

1. **Offline Processing**: Final decision on whether to enable offline capability in Phase 1 or defer to Phase 2
2. **Phone Validation During KYC**: Confirm regulatory requirement vs. volume impact trade-off
3. **Tax ID Field**: Determine if truly mandatory or can be optional to reduce friction
4. **Multi-State Receipts**: Complete validation of receipt requirements for all 42 states
5. **Collections Response Categories**: Finalize the complete list of case categorizations
6. **Rules Builder**: Confirm scope and priority for Phase 1 vs. Phase 2
7. **Reporting Module**: Define specific reports, frequency, and distribution lists
8. **Letter Generation**: Confirm Phase 2 scope for automated letter mailing
9. **Technology Stack**: Finalize platform and technology selections
10. **Timeline and Budget**: Establish project timeline and budget constraints
11. **Issuer Validation**: Clarify process for validating issuer (check writer) identity
12. **Bank Catalog Maintenance**: Define process and responsibility for monthly bank updates
13. **Commission Structure**: Finalize agent commission calculation formula
14. **Supervisor Override Rules**: Define approval hierarchy for various override scenarios

---

## 17. Appendices

### Appendix A: Glossary

- **AML**: Anti-Money Laundering
- **BSA**: Bank Secrecy Act
- **BRD**: Business Requirements Document
- **Cronos**: Back-office platform for Maxi
- **CTR**: Currency Transaction Report
- **Deny List**: Blacklist of customers/issuers prohibited from service
- **Hermes 2.0**: Front-end agent platform for Maxi
- **KYC**: Know Your Customer
- **Mitek**: OCR technology for check scanning
- **Nemesis**: Compliance rules engine and OFAC screening system
- **OCR**: Optical Character Recognition
- **OFAC**: Office of Foreign Assets Control
- **PRD**: Product Requirements Document
- **SAR**: Suspicious Activity Report
- **Valid Systems**: Third-party check validation service
- **X9**: Standard file format for electronic check processing

---

### Appendix B: Reference Documents

The following documents were analyzed to create this BRD:

1. **Transcript Files** (Requirements Discovery Calls):
   - Entendimiento del alcance de Check Cashing - 2025_06_30 (Part 1)
   - Entendimiento del alcance de Check Cashing parte 2 - 2025_07_02
   - Entendimiento del alcance de Check Cashing parte 3 - 2025_07_07
   - Entendimiento del alcance de Check Cashing parte 4 - 2025_07_08

2. **Process Documentation**:
   - Proceso General por departamento.pdf
   - Flujos por Departamento.pdf

3. **Screen Designs**:
   - Diagrama de pantallas.pdf (15 wireframe pages)

---

### Appendix C: Stakeholder Contact Information

*(To be populated with actual stakeholder contact details)*

---

### Appendix D: Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | January 28, 2026 | Development Team | Initial BRD created from discovery call transcripts and design documents |

---

**Document Status:** DRAFT - Pending Stakeholder Review  
**Next Steps:** Review with stakeholders, address outstanding items, finalize requirements

---

*End of Business Requirements Document*
