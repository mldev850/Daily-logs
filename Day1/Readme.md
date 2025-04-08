# Nginx 
# 🚀 HTTP Status Codes Cheat Sheet for Developers

## ✅ 2xx – Success
| Code | Meaning             | Dev Tip / Analogy                               |
|------|---------------------|--------------------------------------------------|
| 200  | OK                  | Request succeeded. Everything's working.         |
| 201  | Created             | New resource created via POST.                  |
| 204  | No Content          | Success, but no data in the response (e.g. DELETE). |

---

## 🔁 3xx – Redirection
| Code | Meaning             | Dev Tip / Analogy                                 |
|------|---------------------|----------------------------------------------------|
| 301  | Moved Permanently   | Resource moved. Update client/bookmarks.          |
| 302  | Found               | Temporary redirect. Don't cache it.               |
| 304  | Not Modified        | Cached content is still valid. Saves bandwidth.   |

---

## ❌ 4xx – Client Errors
| Code | Meaning             | Dev Tip / Analogy                                    |
|------|---------------------|-------------------------------------------------------|
| 400  | Bad Request         | Syntax or validation issue. Check client input.       |
| 401  | Unauthorized        | Login or token required.                             |
| 403  | Forbidden           | Authenticated but lacks permissions.                 |
| 404  | Not Found           | Resource or endpoint doesn’t exist.                  |
| 405  | Method Not Allowed  | Wrong HTTP method (e.g., POST on a GET route).       |
| 429  | Too Many Requests   | Rate limit exceeded. Add retry/backoff logic.        |

---

## 💥 5xx – Server Errors
| Code | Meaning               | Dev Tip / Analogy                                       |
|------|-----------------------|----------------------------------------------------------|
| 500  | Internal Server Error | Bug or crash in the server. Check backend logs.         |
| 502  | Bad Gateway           | Proxy received invalid response.                        |
| 503  | Service Unavailable   | Server is down or overloaded. Try again later.          |
| 504  | Gateway Timeout       | Server took too long to respond (e.g., DB/API timeout). |

