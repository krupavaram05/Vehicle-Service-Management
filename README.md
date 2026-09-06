# Vehicle Service Management — Pega Application

**Author:** Krupavaram Pamula
**Course:** B.Tech, CSE-AIML — Mohan Babu University
**Platform:** Pega Platform (NIP Project)
**Application Name:** NIP-VEHICLE SERVICE-KRUPAVARAM PAMULA
**Case Type:** Vehicle Service Request

## Overview

Vehicle Service Management is a Pega Platform case-management application that automates the complete lifecycle of a vehicle service request — from initial customer submission through inspection, cost estimation, approval, technician assignment, and final resolution.

## Case Flow

**Request Intake → Inspection → Approval → Service Execution → Resolution**
(with an alternate rejection branch from Approval)

1. **Request Intake** – Customer submits Vehicle ID, Vehicle Model, and Issue Description with validation.
2. **Inspection** – Service Advisor records inspection notes and a condition rating.
3. **Approval** – Labor Cost and Parts Cost are entered; Total Cost is auto-calculated. Customer reviews and approves or rejects.
4. **Service Execution** – Case is routed to the correct technician queue based on vehicle type; technician completes the work.
5. **Resolution** – Case is marked complete and the customer is notified via automated correspondence.

## Key Design Decisions

- **Declare Expression for Total Cost** — recalculates automatically whenever Labor or Parts costs change, removing manual math and keeping data consistent.
- **Business logic routing by vehicle type** — routes cases to `HeavyVehicleQueue` or `LightVehicleQueue` automatically, since heavy and light vehicles need different bays, tools, and technician skill sets.

## Data Model

**Vehicle** (reusable data object): Vehicle ID, Model, Type, Registration Number

## SLA

Goal: 2 days · Deadline: 3 days (configured on the case type)

## Personas

- Customer
- Service Advisor
- Technician

## Work Queues

| Queue | Routing Condition |
|---|---|
| HeavyVehicleQueue | Vehicle Type = Heavy |
| LightVehicleQueue | Default / otherwise |

## Key Rules

| Rule Name | Rule Type |
|---|---|
| Total Cost | Declare Expression |
| Vehicle Service Request SLA | Service Level Agreement |
| Route by Vehicle Type | Business Logic Router / Decision Table |
