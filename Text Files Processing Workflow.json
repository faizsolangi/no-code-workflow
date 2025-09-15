{
  "name": "Text Files Processing Workflow",
  "nodes": [
    {
      "parameters": {
        "pollTimes": {
          "item": [
            {
              "mode": "everyMinute"
            }
          ]
        },
        "triggerOn": "specificFolder",
        "folderToWatch": {
          "__rl": true,
          "mode": "id",
          "value": "1iarvM1BQ8sQNNT-XC6KqLqyyfnrY-2hQ"
        },
        "event": "fileCreated",
        "options": {}
      },
      "type": "n8n-nodes-base.googleDriveTrigger",
      "typeVersion": 1,
      "position": [
        -384,
        0
      ],
      "id": "ef575de4-5475-41fb-ac91-23a0eb6dfa1a",
      "name": "Google Drive Trigger",
      "credentials": {
        "googleDriveOAuth2Api": {
          "id": "aZjoBpBpJAzsRImL",
          "name": "Google Drive account"
        }
      }
    },
    {
      "parameters": {
        "operation": "download",
        "fileId": {
          "__rl": true,
          "mode": "id",
          "value": "1qRId9bBz03PlX9rLKlvkuhWbjnK2D7iy"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleDrive",
      "typeVersion": 3,
      "position": [
        -176,
        0
      ],
      "id": "47f551a3-e8a3-49bf-81c1-b0b9659b544c",
      "name": "Download file",
      "alwaysOutputData": true,
      "retryOnFail": true,
      "credentials": {
        "googleDriveOAuth2Api": {
          "id": "aZjoBpBpJAzsRImL",
          "name": "Google Drive account"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "// Code node (JavaScript)\nconst out = [];\n\nfor (let i = 0; i < items.length; i++) {\n  // get binary buffer named 'data' (default for download)\n  const buffer = await this.helpers.getBinaryDataBuffer(i, 'data');\n  const text = buffer.toString('utf8');\n\n  // tweak the regex list to include your target keywords/phrases\n  const keywords = (text.match(/\\b(AI|automation|workflow|data|email)\\b/gi) || []).map(k => k.toLowerCase());\n\n  out.push({\n    json: {\n      filename: $input.first().json.originalFilename || $input.first().json.parents[0],\n      text,\n      keywords\n    }\n  });\n}\n\nreturn out;\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        32,
        0
      ],
      "id": "5d3ee414-563e-4341-b563-141ce3b6db17",
      "name": "Code in JavaScript"
    },
    {
      "parameters": {
        "operation": "append",
        "documentId": {
          "__rl": true,
          "value": "1aMUElkn_dh7L4GoIYOAoIMsuztDhHXOvAConRCXvnTw",
          "mode": "list",
          "cachedResultName": "n8n-t",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1aMUElkn_dh7L4GoIYOAoIMsuztDhHXOvAConRCXvnTw/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Sheet1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1aMUElkn_dh7L4GoIYOAoIMsuztDhHXOvAConRCXvnTw/edit#gid=0"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "filename": "={{ $json.filename }}",
            "text": "={{ $json.text }}",
            "keywords": "={{ $json.keywords }}"
          },
          "matchingColumns": [],
          "schema": [
            {
              "id": "filename",
              "displayName": "filename",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "text",
              "displayName": "text",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "keywords",
              "displayName": "keywords",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {
          "cellFormat": "USER_ENTERED"
        }
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        240,
        0
      ],
      "id": "4d58bdc3-9823-45a0-aa49-5d918446c618",
      "name": "Append row in sheet",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "At9jB3iRWiyD6tM0",
          "name": "Google Sheets account"
        }
      }
    },
    {
      "parameters": {
        "sendTo": "faizsolangi@gmail.com",
        "subject": "Summary — extracted keywords from latest files",
        "message": "=Text: {{ $json.text }},\n\nKeywords: {{ $json.keywords }}",
        "options": {}
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.1,
      "position": [
        448,
        0
      ],
      "id": "66e13453-9fce-4db4-9a84-b03c4bc4745d",
      "name": "Send a message",
      "webhookId": "1281a39a-5d99-4081-af5a-e065606a74fc",
      "credentials": {
        "gmailOAuth2": {
          "id": "q93ba9x0BGukXAnL",
          "name": "Gmail account"
        }
      }
    }
  ],
  "pinData": {},
  "connections": {
    "Google Drive Trigger": {
      "main": [
        [
          {
            "node": "Download file",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Download file": {
      "main": [
        [
          {
            "node": "Code in JavaScript",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Code in JavaScript": {
      "main": [
        [
          {
            "node": "Append row in sheet",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Append row in sheet": {
      "main": [
        [
          {
            "node": "Send a message",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": true,
  "settings": {
    "executionOrder": "v1"
  },
  "versionId": "8d9f4083-0435-4fbc-9eb0-67dcee74f47c",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "78d493c24be73fc3c1f2bb7cb5c7acfadc5514aace380a08a98cec0d440f24b1"
  },
  "id": "A212EIpBqUjyo7DI",
  "tags": []
}