# DHCP Scope Exhaustion

## Problem

A customer contacted our service desk because several employees had suddenly lost network connectivity and were unable to work. One of the affected users was the company president, making the outage both operationally and business critical.

Because the customer requested immediate onsite assistance, I traveled to the location while coordinating with a Tier III engineer remotely.

---

## Business Impact

* Multiple employees unable to work.
* Executive leadership affected.
* Business operations disrupted.
* High-priority customer outage.

---

## Investigation

After arriving onsite, I verified the symptoms and worked with the Tier III engineer to review potential causes.

Rather than replacing hardware or making unnecessary configuration changes, we reviewed the available IP address pool and discovered the DHCP scope had been exhausted.

---

## Root Cause

The DHCP address pool had no available leases remaining, preventing new devices from receiving IP addresses.

---

## Resolution

The Tier III engineer cleared unused leases and adjusted the DHCP configuration to restore address availability.

Once new leases were issued, affected users regained network connectivity and business operations resumed.

After service was restored, I explained the issue to customer leadership using non-technical language so they understood both what happened and why it occurred.

---

## Lessons Learned

* Validate resource exhaustion before assuming hardware failure.
* Collaboration often resolves problems faster than working alone.
* Clear communication is just as important as technical troubleshooting during business-critical incidents.
* Explaining technical issues in relatable language builds confidence and trust with customers.
