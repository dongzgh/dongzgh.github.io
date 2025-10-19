---
title: How to Login Personal Azure Account
permalink: /blogs/how-to-login-personal-azure-account
medium: blog
category: how-to
---

## Why This Happens

The Azure portal at [portal.azure.com](https://portal.azure.com) serves two different types of users:

1. **Organizational Users:** People using an account given to them by their company, school, or other organization (e.g., `yourname@yourcompany.com`). This account lives in the organization's Microsoft Entra ID (formerly Azure AD).
2. **Personal Users:** People using their own consumer Microsoft account to manage their own individual Azure subscriptions.

While both can use the same portal URL, you are likely encountering one of two issues:

* **Issue A: You are on the wrong login page.** The portal has "detected" an organizational tenant and is forcing you to log in with a work account.
* **Issue B: You are using the correct account, but the portal is "stuck" trying to log you into an organization.**

---

## How to Fix It

1. **Close all browser windows** completely.
2. Open a new **InPrivate (Edge) or Incognito (Chrome) window**. This ensures no cached organizational login sessions interfere.
3. Go to this specific URL: **`https://portal.azure.com/?livesignin=1`**
    * The `?livesignin=1` parameter tells Azure to redirect to the personal account login flow.
4. Now, enter your **personal account email address** (e.g., <yourname@outlook.com>).
