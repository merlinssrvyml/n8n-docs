---
title: n8n Hosting Documentation and Guides
description: Access n8n hosting documentation and guides. Find comprehensive resources to help you set up and manage your self-hosted n8n instances.
contentType: overview
hide:
  - toc
  - feedback
  - kapaButton
---

# Self-hosting n8n

This section provides guidance on setting up n8n for both the Enterprise and Community self-hosted editions. The Community edition is free, the Enterprise edition isn't. 

See [Community edition features](/hosting/community-edition-features.md) for a list of available features. 

<div class="grid-cards-vertical cards" markdown>

- __Installation and server setups__

	Install n8n on any platform using npm or Docker. Or follow our guides to popular hosting platforms.

	[:octicons-arrow-right-24: Docker installation guide](/hosting/installation/docker.md)

- __Configuration__

	Learn how to configure n8n with environment variables.

	[:octicons-arrow-right-24: Environment Variables](/hosting/configuration/environment-variables/index.md)

- __Users and authentication__

	Choose and set up user authentication for your n8n instance.

	[:octicons-arrow-right-24: Authentication](/hosting/configuration/user-management-self-hosted.md)

- __Scaling__

	Manage data, modes, and processes to keep n8n running smoothly at scale.

	[:octicons-arrow-right-24: Scaling](/hosting/scaling/queue-mode.md)

- __Securing n8n__

	Secure your n8n instance by setting up SSL, SSO, or 2FA or blocking or opting out of some data collection or features.

	[:octicons-arrow-right-24: Securing n8n guide](/hosting/securing/overview.md)

- __Starter kits__

	New to n8n or AI? Try our Self-hosted AI Starter Kit. Curated by n8n, it combines the self-hosted n8n platform with compatible AI products and components to get you started building self-hosted AI workflows.

	[:octicons-arrow-right-24: Starter kits](/hosting/starter-kits/ai-starter-kit.md)

</div>

--8<-- "_snippets/self-hosting/warning.md"
{
  "meta": {
    "instanceId": "67d4d33d8b0ad4e5e12f051d8ad92fc35893d7f48d7f801bc6da4f39967b3592"
  },
  "nodes": [
    {
      "id": "30f5203b-469d-4f0c-8493-e8f08e14e4fe",
      "name": "When clicking ‘Test workflow’",
      "type": "n8n-nodes-base.manualTrigger",
      "position": [
        -560,
        440
      ],
      "parameters": {},
      "typeVersion": 1
    },
    {
      "id": "d16f59dd-f54e-487b-9aac-67f109ba9869",
      "name": "Sticky Note8",
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        1000,
        -280
      ],
      "parameters": {
        "color": 7,
        "width": 727.9032097745135,
        "height": 110.58643966444157,
        "content": "# Auto Categorise Outlook Emails with AI\nBuilt by [Wayne Simpson](https://www.linkedin.com/in/simpsonwayne/) at [nocodecreative.io](https://nocodecreative.io)"
      },
      "typeVersion": 1
    },
    {
      "id": "4e110412-8530-4322-bc5c-7f9df2b63bcb",
      "name": "Sticky Note9",
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        1100,
        -120
      ],
      "parameters": {
        "color": 7,
        "width": 506.8102696237577,
        "height": 337.24177957113216,
        "content": "### Watch Set Up Video 👇\n[![Auto Categorise Outlook Emails with AI](https://vdyfnvnstovfxpabhdjc.supabase.co/storage/v1/object/public/images/Thumbnails/auto-categories-emails.png?t=2024-10-11T09%3A56%3A37.961Z#full-width)](https://www.youtube.com/watch?v=EhRBkkjv_3c)\n\n"
      },
      "typeVersion": 1
    },
    {
      "id": "9d79875f-148e-46ef-967a-95c07298456d",
      "name": "Ollama Chat Model1",
      "type": "@n8n/n8n-nodes-langchain.lmChatOllama",
      "position": [
        1129,
        684
      ],
      "parameters": {
        "model": "qwen2.5:14b",
        "options": {
          "temperature": 0.2
        }
      },
      "typeVersion": 1
    },
    {
      "id": "bcf92a71-ff5f-46a7-bec3-cedb5be2bf98",
      "name": "Microsoft Outlook10",
      "type": "n8n-nodes-base.microsoftOutlook",
      "position": [
        3020,
        8
      ],
      "parameters": {
        "folderId": {
          "__rl": true,
          "mode": "list",
          "value": "AQMkAGE3ZTU5MGMzLTFkNGItNGQ5Zi04MDQ1LThmNGFlMTVhYjMwYgAuAAAD8UhruVwm402lgPBG2Tj-aQEAnz-IOcWBGE2lrVuQgAF6zAAAAgFJAAAA",
          "cachedResultUrl": "https://outlook.office365.com/mail/AQMkAGE3ZTU5MGMzLTFkNGItNGQ5Zi04MDQ1LThmNGFlMTVhYjMwYgAuAAAD8UhruVwm402lgPBG2Tj%2FaQEAnz%2FIOcWBGE2lrVuQgAF6zAAAAgFJAAAA",
          "cachedResultName": "Junk Email"
        },
        "messageId": {
          "__rl": true,
          "mode": "id",
          "value": "={{ $('varID & Category1').item.json.id }}"
        },
        "operation": "move"
      },
      "typeVersion": 2
    },
    {
      "id": "100db1cb-3819-43c7-a74b-5c087ad4f2da",
      "name": "Microsoft Outlook12",
      "type": "n8n-nodes-base.microsoftOutlook",
      "position": [
        2700,
        8
      ],
      "parameters": {
        "messageId": {
          "__rl": true,
          "mode": "id",
          "value": "={{ $('varID & Category1').item.json.id }}"
        },
        "operation": "update",
        "updateFields": {
          "categories": "={{ \n  [$('varJSON1').first().json.output.category, $('varJSON1').first().json.output.subCategory]\n    .filter(item => item && item.trim() !== \"\")\n    .map(item => item.charAt(0).toUpperCase() + item.slice(1))\n}}"
        }
      },
      "typeVersion": 2
    },
    {
      "id": "d4969259-a3ae-473d-82ef-0c9f7933c899",
      "name": "Loop Over Items1",
      "type": "n8n-nodes-base.splitInBatches",
      "position": [
        160,
        448
      ],
      "parameters": {
        "options": {}
      },
      "typeVersion": 3
    },
    {
      "id": "524f6be3-7708-4aae-b9ab-e0ef8180a627",
      "name": "Microsoft Outlook13",
      "type": "n8n-nodes-base.microsoftOutlook",
      "position": [
        2700,
        188
      ],
      "parameters": {
        "messageId": {
          "__rl": true,
          "mode": "id",
          "value": "={{ $('varID & Category1').item.json.id }}"
        },
        "operation": "update",
        "updateFields": {
          "categories": "={{ \n  [$('varJSON1').first().json.output.category, $('varJSON1').first().json.output.subCategory]\n    .filter(item => item && item.trim() !== \"\")\n    .map(item => item.charAt(0).toUpperCase() + item.slice(1))\n}}"
        }
      },
      "typeVersion": 2
    },
    {
      "id": "72cb54f3-4e4e-4ad2-8845-11a38fc29f1a",
      "name": "Microsoft Outlook15",
      "type": "n8n-nodes-base.microsoftOutlook",
      "position": [
        3020,
        188
      ],
      "parameters": {
        "folderId": {
          "__rl": true,
          "mode": "list",
          "value": "AQMkAGE3ZTU5MGMzLTFkNGItNGQ5Zi04MDQ1LThmNGFlMTVhYjMwYgAuAAAD8UhruVwm402lgPBG2Tj-aQEAnz-IOcWBGE2lrVuQgAF6zAADLJmrBwAAAA==",
          "cachedResultUrl": "https://outlook.office365.com/mail/AQMkAGE3ZTU5MGMzLTFkNGItNGQ5Zi04MDQ1LThmNGFlMTVhYjMwYgAuAAAD8UhruVwm402lgPBG2Tj%2FaQEAnz%2FIOcWBGE2lrVuQgAF6zAADLJmrBwAAAA%3D%3D",
          "cachedResultName": "Receipt"
        },
        "messageId": {
          "__rl": true,
          "mode": "id",
          "value": "={{ $('varID & Category1').item.json.id }}"
        },
        "operation": "move"
      },
      "typeVersion": 2
    },
    {
      "id": "e4446e84-c05e-4d04-b415-7608e39024ee",
      "name": "Microsoft Outlook16",
      "type": "n8n-nodes-base.microsoftOutlook",
      "position": [
        2709,
        504
      ],
      "parameters": {
        "messageId": {
          "__rl": true,
          "mode": "id",
          "value": "={{ $('varID & Category1').item.json.id }}"
        },
        "operation": "update",
        "updateFields": {
          "categories": "={{ \n  [$('varJSON1').first().json.output.category, $('varJSON1').first().json.output.subCategory]\n    .filter(item => item && item.trim() !== \"\")\n    .map(item => item.charAt(0).toUpperCase() + item.slice(1))\n}}"
        }
      },
      "typeVersion": 2
    },
    {
      "id": "3ee05cfe-a528-472e-aa3d-c890fd88b6c4",
      "name": "Microsoft Outlook17",
      "type": "n8n-nodes-base.microsoftOutlook",
      "position": [
        3020,
        508
      ],
      "parameters": {
        "folderId": {
          "__rl": true,
          "mode": "list",
          "value": "AQMkAGE3ZTU5MGMzLTFkNGItNGQ5Zi04MDQ1LThmNGFlMTVhYjMwYgAuAAAD8UhruVwm402lgPBG2Tj-aQEAnz-IOcWBGE2lrVuQgAF6zAADLJmrCAAAAA==",
          "cachedResultUrl": "https://outlook.office365.com/mail/AQMkAGE3ZTU5MGMzLTFkNGItNGQ5Zi04MDQ1LThmNGFlMTVhYjMwYgAuAAAD8UhruVwm402lgPBG2Tj%2FaQEAnz%2FIOcWBGE2lrVuQgAF6zAADLJmrCAAAAA%3D%3D",
          "cachedResultName": "Community"
        },
        "messageId": {
          "__rl": true,
          "mode": "id",
          "value": "={{ $('varID & Category1').item.json.id }}"
        },
        "operation": "move"
      },
      "typeVersion": 2
    },
    {
      "id": "2fcecd9e-95cc-489a-b874-699c54518e44",
      "name": "Microsoft Outlook18",
      "type": "n8n-nodes-base.microsoftOutlook",
      "position": [
        2709,
        344
      ],
      "parameters": {
        "messageId": {
          "__rl": true,
          "mode": "id",
          "value": "={{ $('varID & Category1').item.json.id }}"
        },
        "operation": "update",
        "updateFields": {
          "categories": "={{ \n  [$('varJSON1').first().json.output.category, $('varJSON1').first().json.output.subCategory]\n    .filter(item => item && item.trim() !== \"\")\n    .map(item => item.charAt(0).toUpperCase() + item.slice(1))\n}}"
        }
      },
      "typeVersion": 2
    },
    {
      "id": "41a39309-1a94-461f-9308-63dd5b9a94a7",
      "name": "Microsoft Outlook19",
      "type": "n8n-nodes-base.microsoftOutlook",
      "position": [
        3020,
        348
      ],
      "parameters": {
        "folderId": {
          "__rl": true,
          "mode": "list",
          "value": "AQMkAGE3ZTU5MGMzLTFkNGItNGQ5Zi04MDQ1LThmNGFlMTVhYjMwYgAuAAAD8UhruVwm402lgPBG2Tj-aQEAnz-IOcWBGE2lrVuQgAF6zAADLJmrCQAAAA==",
          "cachedResultUrl": "https://outlook.office365.com/mail/AQMkAGE3ZTU5MGMzLTFkNGItNGQ5Zi04MDQ1LThmNGFlMTVhYjMwYgAuAAAD8UhruVwm402lgPBG2Tj%2FaQEAnz%2FIOcWBGE2lrVuQgAF6zAADLJmrCQAAAA%3D%3D",
          "cachedResultName": "SaaS"
        },
        "messageId": {
          "__rl": true,
          "mode": "id",
          "value": "={{ $('varID & Category1').item.json.id }}"
        },
        "operation": "move"
      },
      "typeVersion": 2
    },
    {
      "id": "ebf606f9-099c-4218-b23b-66e2487262d0",
      "name": "Markdown1",
      "type": "n8n-nodes-base.markdown",
      "notes": "Converts the body of the email to markdown",
      "position": [
        420,
        468
      ],
      "parameters": {
        "html": "={{ $('Loop Over Items1').item.json.body.content }}",
        "options": {}
      },
      "notesInFlow": true,
      "typeVersion": 1
    },
    {
      "id": "ff447dd5-3ef6-4a02-8453-3489af8bf6b5",
      "name": "varEmal1",
      "type": "n8n-nodes-base.set",
      "notes": "Set email fields",
      "position": [
        620,
        468
      ],
      "parameters": {
        "options": {},
        "assignments": {
          "assignments": [
            {
              "id": "edb304e1-3e9f-4a77-918c-25646addbc53",
              "name": "subject",
              "type": "string",
              "value": "={{ $json.subject }}"
            },
            {
              "id": "57a3ef3a-2701-40d9-882f-f43a7219f148",
              "name": "importance",
              "type": "string",
              "value": "={{ $json.importance }}"
            },
            {
              "id": "d8317f4f-aa0e-4196-89af-cb016765490a",
              "name": "sender",
              "type": "object",
              "value": "={{ $json.sender.emailAddress }}"
            },
            {
              "id": "908716c8-9ff7-4bdc-a1a3-64227559635e",
              "name": "from",
              "type": "object",
              "value": "={{ $json.from.emailAddress }}"
            },
            {
              "id": "ce007329-e221-4c5a-8130-2f8e9130160f",
              "name": "body",
              "type": "string",
              "value": "={{ $json.data\n    .replace(/<[^>]*>/g, '')                      // Remove HTML tags\n    .replace(/\\[(.*?)\\]\\((.*?)\\)/g, '')            // Remove Markdown links like [text](link)\n    .replace(/!\\[.*?\\]\\(.*?\\)/g, '')               // Remove Markdown images like ![alt](image-link)\n    .replace(/\\|/g, '')                            // Remove table separators \"|\"\n    .replace(/-{3,}/g, '')                         // Remove horizontal rule \"---\"\n    .replace(/\\n+/g, ' ')                          // Remove multiple newlines\n    .replace(/([^\\w\\s.,!?@])/g, '')                // Remove special characters except essential ones\n    .replace(/\\s{2,}/g, ' ')                       // Replace multiple spaces with a single space\n    .trim()                                        // Trim leading/trailing whitespace\n}}\n"
            }
          ]
        }
      },
      "typeVersion": 3.4
    },
    {
      "id": "198524cb-c9f0-4261-8c38-7c878efe7457",
      "name": "Microsoft Outlook20",
      "type": "n8n-nodes-base.microsoftOutlook",
      "position": [
        2700,
        668
      ],
      "parameters": {
        "messageId": {
          "__rl": true,
          "mode": "id",
          "value": "={{ $('varID & Category1').item.json.id }}"
        },
        "operation": "update",
        "updateFields": {
          "categories": "={{ \n  [$('varJSON1').first().json.output.category, $('varJSON1').first().json.output.subCategory]\n    .filter(item => item && item.trim() !== \"\")\n    .map(item => item.charAt(0).toUpperCase() + item.slice(1))\n}}"
        }
      },
      "typeVersion": 2
    },
    {
      "id": "ec73629c-59ac-4f0e-a432-2c06934952ab",
      "name": "Microsoft Outlook21",
      "type": "n8n-nodes-base.microsoftOutlook",
      "position": [
        2709,
        1044
      ],
      "parameters": {
        "messageId": {
          "__rl": true,
          "mode": "id",
          "value": "={{ $('varID & Category1').item.json.id }}"
        },
        "operation": "update",
        "updateFields": {
          "categories": "={{ \n  [$('varJSON1').first().json.output.category, $('varJSON1').first().json.output.subCategory]\n    .filter(item => item && item.trim() !== \"\")\n    .map(item => item.charAt(0).toUpperCase() + item.slice(1))\n}}"
        }
      },
      "typeVersion": 2
    },
    {
      "id": "0a19d15c-0cd3-4f26-9be2-4914522751fb",
      "name": "Filter1",
      "type": "n8n-nodes-base.filter",
      "position": [
        -100,
        448
      ],
      "parameters": {
        "options": {},
        "conditions": {
          "options": {
            "version": 2,
            "leftValue": "",
            "caseSensitive": true,
            "typeValidation": "strict"
          },
          "combinator": "and",
          "conditions": [
            {
              "id": "c8cd6917-f94e-4fb7-8601-b8ed8f1aa8bf",
              "operator": {
                "type": "array",
                "operation": "empty",
                "singleValue": true
              },
              "leftValue": "={{ $json.categories }}",
              "rightValue": ""
            }
          ]
        }
      },
      "typeVersion": 2.2
    },
    {
      "id": "96e6e31c-6306-44a8-a57a-2b5216636b00",
      "name": "If1",
      "type": "n8n-nodes-base.if",
      "notes": "Checks if the email has been read",
      "position": [
        3320,
        668
      ],
      "parameters": {
        "options": {},
        "conditions": {
          "options": {
            "version": 2,
            "leftValue": "",
            "caseSensitive": true,
            "typeValidation": "strict"
          },
          "combinator": "and",
          "conditions": [
            {
              "id": "f8cf2a56-cea8-4150-b7a0-048dbda20f2f",
              "operator": {
                "type": "boolean",
                "operation": "true",
                "singleValue": true
              },
              "leftValue": "={{ $json.isRead }}",
              "rightValue": ""
            }
          ]
        }
      },
      "typeVersion": 2.2
    },
    {
      "id": "8a6e0118-abe3-45e2-aefc-94640348b2ec",
      "name": "Microsoft Outlook22",
      "type": "n8n-nodes-base.microsoftOutlook",
      "position": [
        2709,
        864
      ],
      "parameters": {
        "messageId": {
          "__rl": true,
          "mode": "id",
          "value": "={{ $('varID & Category1').item.json.id }}"
        },
        "operation": "update",
        "updateFields": {
          "categories": "={{ \n  [$('varJSON1').first().json.output.category, $('varJSON1').first().json.output.subCategory]\n    .filter(item => item && item.trim() !== \"\")\n    .map(item => item.charAt(0).toUpperCase() + item.slice(1))\n}}"
        }
      },
      "typeVersion": 2
    },
    {
      "id": "e2d8e7b5-4447-4327-9f4e-b8d52765667e",
      "name": "Catch Errors1",
      "type": "n8n-nodes-base.set",
      "position": [
        1760,
        608
      ],
      "parameters": {
        "options": {},
        "assignments": {
          "assignments": [
            {
              "id": "0dc6d439-60fb-49f6-b4d5-f5cce6f030ad",
              "name": "error",
              "type": "string",
              "value": "={{ $json }}"
            }
          ]
        }
      },
      "typeVersion": 3.4
    },
    {
      "id": "17f6ac43-51e4-4bee-b0d8-13deb3bf3cc9",
      "name": "varJSON1",
      "type": "n8n-nodes-base.set",
      "onError": "continueErrorOutput",
      "position": [
        1540,
        468
      ],
      "parameters": {
        "options": {
          "ignoreConversionErrors": true
        },
        "assignments": {
          "assignments": [
            {
              "id": "0c52f57f-74eb-4385-ac6b-f3e5f4f50e73",
              "name": "output",
              "type": "object",
              "value": "={{ $json.output.replace(/^.*?({.*}).*$/s, '$1') }}"
            }
          ]
        }
      },
      "typeVersion": 3.4
    },
    {
      "id": "82dd9631-a34b-4d54-be28-6f8dcc3548f0",
      "name": "Sticky Note10",
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        -360,
        220
      ],
      "parameters": {
        "width": 411.91693012378937,
        "height": 401.49417117683515,
        "content": "## Outlook Business with filters\nFilters:\n```\nflag/flagStatus eq 'notFlagged' and not categories/any()\n```\n\nThese filters ensure we do not process flagged emails or email that already have a category set."
      },
      "typeVersion": 1
    },
    {
      "id": "0583e196-37a5-43db-8c0a-aa624029c926",
      "name": "Microsoft Outlook23",
      "type": "n8n-nodes-base.microsoftOutlook",
      "position": [
        -300,
        448
      ],
      "parameters": {
        "limit": 1,
        "fields": [
          "flag",
          "from",
          "importance",
          "replyTo",
          "sender",
          "subject",
          "toRecipients",
          "body",
          "categories",
          "isRead"
        ],
        "output": "fields",
        "options": {},
        "filtersUI": {
          "values": {
            "filters": {
              "custom": "flag/flagStatus eq 'notFlagged' and not categories/any()",
              "foldersToInclude": [
                "AQMkAGE3ZTU5MGMzLTFkNGItNGQ5Zi04MDQ1LThmNGFlMTVhYjMwYgAuAAAD8UhruVwm402lgPBG2Tj-aQEAnz-IOcWBGE2lrVuQgAF6zAAAAgEMAAAA"
              ]
            }
          }
        },
        "operation": "getAll"
      },
      "typeVersion": 2
    },
    {
      "id": "a9540e6b-929b-4460-8972-93e4d19cd934",
      "name": "varID & Category1",
      "type": "n8n-nodes-base.set",
      "position": [
        900,
        468
      ],
      "parameters": {
        "options": {},
        "assignments": {
          "assignments": [
            {
              "id": "de2ad4f2-7381-4715-a3f4-59611e161b74",
              "name": "id",
              "type": "string",
              "value": "={{ $('Microsoft Outlook23').item.json.id }}"
            },
            {
              "id": "458c7a89-e4a3-46d0-8b38-72d87748e306",
              "name": "category",
              "type": "string",
              "value": "\"action\", \"junk\", \"receipt\", \"SaaS\", \"community\", \"business\" or \"other\""
            }
          ]
        }
      },
      "typeVersion": 3.4
    },
    {
      "id": "e6b3b41e-d7d3-4c9b-8189-a005c748ff18",
      "name": "Sticky Note11",
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        360,
        348
      ],
      "parameters": {
        "color": 6,
        "width": 418.7820408163265,
        "height": 301.40952380952365,
        "content": "## Sanitise Email \nRemoves HTML and useless information in preparation for the AI Agent"
      },
      "typeVersion": 1
    },
    {
      "id": "f9787a75-526c-4ef1-b0a7-0db7d890ab3f",
      "name": "Sticky Note12",
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        820,
        348
      ],
      "parameters": {
        "color": 6,
        "width": 256.16108843537415,
        "height": 298.37931972789124,
        "content": "## Modify Categories \nEdit this to customise category selection"
      },
      "typeVersion": 1
    },
    {
      "id": "50223a01-34cf-4191-9dd7-3dac02a9e945",
      "name": "Sticky Note13",
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        1480,
        328
      ],
      "parameters": {
        "color": 5,
        "width": 441.003537414966,
        "height": 463.0204081632651,
        "content": "## Convert to JSON\n* Ensures the Agent output to converted to JSON\n* Catches any errors and continues
		
