
# Mother’s Secret – TryHackMe

## Date
22 February 2026

## Objective
Mother's Secret is a CTF (Capture The Flag) challenge focused on Web Exploitation and Information Disclosure. The objective was to investigate 
a web application related to the "Nostromo" ship (from the Alien franchise) to uncover hidden secrets across different levels of access.

## What I Did
- Inspected page source
- Used directory brute-forcing
- Found hidden resources

## Tools & Skills Used
- Reconnaissance: Browser DevTools, Directory Brute-forcing.
- Web Analysis: Source code inspection (JavaScript), API endpoint testing.
- Exploitation: Exploiting improper routing and hidden API parameters.
- Problem Solving: Decoding hints and navigating multi-stage web logic.

## Key Phases of the Attack
1. Enumeration & Discovery
The initial phase involved exploring the web interface. By inspecting the Page Source, I discovered references
 to how the application handles requests. Key findings included:
- Identifying the backend framework (Node.js/Express).
- Locating a specific JavaScript file responsible for the "Muthur" interface.

2. API Exploration
I analyzed the client-side code to understand how it talked to the server. I found an API endpoint: /api/v1/updates. 
By testing this endpoint with different parameters, I was able to trigger responses that weren't visible through the standard UI.

3. Exploiting Information Disclosure
The core vulnerability was Sensitive Data Exposure within the application's source code and API responses.
- Task 1: Found via initial site exploration and basic source inspection.
- Task 2: Required identifying a hidden "Order" or "Secret" parameter within the API call.
- Task 3: Involved deeper analysis of the JSON responses to find the final hidden flag.

## Key Learning
- Client-Side Logic is Not Secret: Any logic or "secret" routes embedded in JavaScript can be easily read by an attacker.
- API Security: Endpoints should be hardened. Even if a UI doesn't show a button, the API might still respond 
  to manual requests (via curl or Burp Suite).
- Small hints in HTML comments matter.
- Enumeration is critical before exploitation.
- Patience is important in CTFs.

## Security Concept
This room demonstrates poor configuration management and improper access control.
