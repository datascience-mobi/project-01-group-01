---
output: github_document
---

# To Do
## Data overview



## Data cleanup

1. remove irrelevant columns:
  + data which are not brain cancer
    ```
    allDepMapData$annotation = allDepMapData$annotation[allDepMapData$annotation$Primary.Disease == "Brain Cancer", ]
    ```
  + (remove source, gender, aliases?) 
2. remove NA values
  + (remove rows with missing values?)

3. assign data formats, make all data nominal (annotation)
```
allDepMapData$annotation$DepMap_ID = factor(allDepMapData$annotation$DepMap_ID)
allDepMapData$annotation$CCLE_Name = factor(allDepMapData$annotation$CCLE_Name)
allDepMapData$annotation$Aliases = factor(allDepMapData$annotation$Aliases)
allDepMapData$annotation$Primary.Disease = factor(allDepMapData$annotation$Primary.Disease)
allDepMapData$annotation$Subtype.Disease = factor(allDepMapData$annotation$Subtype.Disease)
allDepMapData$annotation$Subtype.Gender = factor(allDepMapData$annotation$Gender)
allDepMapData$annotation$Subtype.Source = factor(allDepMapData$annotation$Source)
```
4. make cell line identifier be the rownames in annotation?
```
rownames(allDepMapData$annotation) = allDepMapData$annotation$DepMap_ID
allDepMapData$annotation = allDepMapData$annotation[, -1]
```

5. remove irrelevant cell lines from the other tables as well
```
cell.lines = dput(rownames(allDepMapData$annotation))
allDepMapData$expression = allDepMapData$expression[, -which(colnames(allDepMapData$expression) %!in% cell.lines)]
# library "operators" is needed for "%!in%"
```