# Checking for JWT in a Node.js Application

To verify the presence of JWT code in a Node.js application using pattern matching, you can employ regular expressions. Follow this approach:

1. Read all files in your Node.js application.
2. Use regular expressions to identify common patterns linked to JWT, such as `jsonwebtoken` or `Bearer`.

Below is a JavaScript script to assist:

```javascript
const fs = require('fs');
const path = require('path');

function searchForJWTInDirectory(directory) {
    const files = fs.readdirSync(directory);

    for (const file of files) {
        const fullPath = path.join(directory, file);
        const stats = fs.statSync(fullPath);

        if (stats.isDirectory()) {
            searchForJWTInDirectory(fullPath);
        } else if (stats.isFile() && (file.endsWith('.js') || file.endsWith('.ts'))) {
            const content = fs.readFileSync(fullPath, 'utf-8');
            if (/jsonwebtoken|Bearer\s+token/i.test(content)) {
                console.log(`JWT-related code found in: ${fullPath}`);
            }
        }
    }
}

const rootDirectory = './'; // starting from current directory
searchForJWTInDirectory(rootDirectory);
```
