# Lab Summary

I started with three deliberately naive zero-shot prompts and ran each one 5, 10, and 15 times at temperature 1, 
which made the failure patterns impossible to miss: 
the sentiment prompt never returned a clean label (13.3% consistency, full sentences with invented categories like "Customer Satisfaction"), 
the extraction prompt produced a different schema on almost every run (field names like "Order Number" vs "Item Number" vs "Order ID"), and 
the product prompt swung between 200- and 400-word descriptions full of hallucinated specs and invented product names. 

Adding explicit output formats, constraints, and controlled vocabularies in v2 was the single biggest win — sentiment jumped to 100% exact-match and extraction to 93.3% even at temperature 1 


— while v3's few-shot examples locked the output shape for sentiment and brought the product description to 100% format adherence (~50 words, fixed feature order). 

The most surprising finding was that Chain-of-Thought was a trade-off, not a free upgrade: it made the extraction reasoning visible and kept the final block 100% parseable, but the variable reasoning text collapsed exact-match consistency from 93.3% to 6.7%, teaching me that CoT output needs to be separated from the machine-readable answer. 

Testing variations in Part 5 exposed what I would do differently next time: I would include realistic Neutral few-shot examples from the start (my template still classified a factual message as Positive 5/5), add a "Not Mentioned" rule for missing fields from the first iteration (it eliminated the hallucinated year "2023"), and build the automated consistency-measurement harness before writing any prompts — measuring by eye on single runs is exactly how the original "working" chatbot prompts made it to production.
