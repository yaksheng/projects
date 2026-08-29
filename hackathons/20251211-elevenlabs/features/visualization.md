# Visualization

## Prototype Behavior

SourceVoice sends structured part and mold context to an image model and displays the result alongside a cost breakdown. The image is intended to support discussion and prompt refinement.

The cost view separates categories such as material, tooling, labor, and overhead. Values depend on user input and model assumptions.

## Limitations

- Generated images are visual references, not CAD models, mold drawings, inspection plans, or manufacturing instructions.
- Dimensions, components, cross-sections, and labels may be incomplete or incorrect.
- Cost values are not supplier quotations and were not benchmarked during the hackathon.
- Model output requires review by qualified engineering and manufacturing personnel.

## Future Work

- Display source assumptions and uncertainty with each result.
- Preserve revisions and link images to the inputs that produced them.
- Add export only with a clear visual-reference designation.
- Evaluate whether users distinguish generated references from engineering drawings.

[Back to overview](../README.md)
