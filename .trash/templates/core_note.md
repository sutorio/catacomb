---
title: {{title}}
created_utc: {{date}} {{time}}
---

<%*
let tags = await tp.system.prompt("Tags", "");
console.log(JSON.stringify(tags));
tp.frontmatter["tags"] = "blurp";
%>