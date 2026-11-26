Overview

Smart Apparel Finder turns a shopper’s product description into a simple search experience. Built with n8n, it collects apparel details through a form, requests marketplace listings, and presents returned products in an easy-to-scan HTML table. Users enter an apparel name, colour, and customer category, then receive listing titles, displayed prices, sources, and direct product links.

The workflow details in this README were verified against the supplied smart-shop.json export. The concise, section-led README style is inspired by the Daily AI Research Digest repository.



✨ Key Features

Form-first search — Collects apparel name (اسم پوشاک), colour (رنگ پوشاک), and category (نوع پوشاک).

Category options — The form currently offers زنانه, مردانه, and بچه گانه.

Torob lookup — An HTTP Request node retrieves marketplace results.

HTML result table — JavaScript prepares an RTL table with source, product name, price, and a direct listing link, which the response Form displays.

Simple architecture — Four connected nodes, no branches, and an editable linear workflow.

Scope note: The supplied export is configured for Torob. Additional marketplaces, strict semantic or colour matching, and cheapest-first sorting require implementation and testing; they are not guaranteed by the current workflow.

⚙️ Workflow Flow

The workflow follows one direct path:

On form submission collects the shopper’s apparel name, colour, and category.

HTTP Request1 sends the search request and receives marketplace data.

Code in JavaScript transforms the response into the HTML markup used by the result page.

Form completes the interaction by showing {{ $json.result }} as text/HTML content.

This linear layout makes troubleshooting straightforward: inspect form values first, then the HTTP response, then the generated HTML. The workflow is currently marked inactive in the supplied export, so it must be activated after configuration. Source: supplied smart-shop.json.

🛠️ Setup

Prerequisites

An n8n instance with Form Trigger, HTTP Request, Code, and Form nodes.

Network access to the marketplace endpoint configured in the HTTP Request node.

Import and run

Import smart-shop.json in n8n.

Review the form fields and verify the endpoint, query parameters, and request limits in HTTP Request1.

Inspect the Code node if changing filtering or table output. Keep the Form response expression aligned with its output: ={{ $json.result }}.

Save and test with representative queries, then activate the workflow. The supplied export is inactive.

Test Persian text rendering on the public form URL before sharing it.

⚠️ Important Notes

Search quality depends on the API. Marketplace results can include related products; exact colour or product-type matching is not guaranteed by the query alone.

Filtering and sorting are explicit logic. For strict matching, add an AND-based check in the Code node. For cheapest-first results, parse prices as numbers and sort before rendering.

Escape external data. Product names and URLs come from an external response. Escape inserted text and validate links before public deployment.

Test edge cases. Check missing colours and similar garment names, such as “sweatshirt” and “hoodie,” against your intended matching rules.

References

Daily AI Research Digest — GitHub README — consulted for README visual style and organization.

smart-shop.json — supplied n8n workflow export, lines 1–166; consulted for the workflow name, node configuration, field labels, connections, response expression, and activation state.

