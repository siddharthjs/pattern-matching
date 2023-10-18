# Checking for Potential IDOR in a Node.js Application

### Explanation of Patterns:

- `req.body.\w+`: Searches for instances where properties from the request body are accessed, such as `req.body.userID`.
  
- `req.params.\w+`: Identifies instances where URL parameters might be in use, possibly indicating route parameters like `/user/:userID`.

- `req.query.\w+`: Detects instances where query parameters are being accessed, for example, `req.query.userID` in a URL like `/user?userID=123`.