# Refactoring-a-Legacy-Account-Opening-System-to-Eliminate-Database-Lock-Contention
## Context

The organization operates a core account opening application used by Relationship Managers (RMs) to onboard customers. The application is hosted on IIS and integrates directly with the Core Banking Application (CBA) via synchronous APIs.

Over the years, the system became increasingly unstable under load, frequently failing during concurrent account opening attempts. The most visible symptom was persistent database lock waits, causing requests to stall indefinitely until application context was refreshed.

This issue had operational, reputational, and productivity impacts across the business.
