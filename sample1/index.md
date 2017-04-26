# OPS Rendering E2E Test cases and descriptions

## Regression automaiton rendering test cases

**Reference repos**: https://github.com/OPS-E2E-PPE/E2E_DocsBranch

Most of these tests are checking the markdown syntax to make sure they're have the correct behavior on the page. You can see the test report [here](./ops-build-e2e/ops-build-e2e-testcases.md#report)

**Test cases behaviors,description and check points**

(./ops-build-e2e/ops-build-e2e-testcases.md#report).

1. [Content/TOC] general: metadata related

    - **Description**:
    - **Check Points**: 
        * Check whether all required metadata are set in of built HTML. 
        * Check whether global metadata in docfx.json takes effect.
        * Check whether certain metadata overrides global settings, such as update_date.

2. [Content/TOC] conceptual MD

    - **Description**: There are many supported syntax in MD contents that should be built correctly.
    - **Check Points**: [INCLUDE], \[](), \[()](), \[](url)

3. [Content/TOC] YAML header

    - **Description**: User defined YAML header should be put into of built HTML.
    - **Check Points**:

4. [Content/TOC] special page: index.md

    - **Description**: 
    - **Check Points**: [TOC] Index in toc: When need normalize index, if the url equal with "index", then replace with "./". if the url ends with "index" then remove it. Example
        * index -> ./
        * a/index -> a/ 
        * a-index -> a-index (no change)

5. [Content/TOC] special page: customized 404 page

    - **Description**:
    - **Check  Points**:
        * Customized 404 page, it should be noindex/nofollow 
        * When visit a page not existed under this docset, it should show customized 404 page instead of default one.

