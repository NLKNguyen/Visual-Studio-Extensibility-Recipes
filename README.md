# Visual Studio Extensibility Recipes
Useful code recipes for developing Visual Studio Extension

To contribute to this page, go [here] (https://github.com/NLKNguyen/Visual-Studio-Extensibility-Recipes/blob/master/README.md) to edit directly and send Pull Request.


## Snapshot, Span, and Classification

**Given:** SnapshotPoint snapshotPoint

**Get:** ITextSnapshot which the snapshotPoint refers to

```C#
ITextSnapshot snapshot = snapshotPoint.Value.Snapshot;
```
----

**Given:** SnapshotPoint snapshotPoint

**Get:**  ITextSnapshotLine at the line that contains snapshotPoint

```C#
ITextSnapshotLine snapshotLine = snapshotPoint.GetContainingLine();
```
----

**Given:** ITextSnapshot snapshot

**Get:**  ITextSnapshotLine at line number

```C#
ITextSnapshotLine snapshotLine = snapshot.GetLineFromLineNumber(42);
```
----

**Given:** ITextSnapshotLine snapshotLine

**Get:** SnapshotPoint of where the line starts and ends 

```C#
SnapshotPoint startPoint = snapshotLine.Start; // file-wise index number - can be used as int
SnapshotPoint endPoint   = snapshotLine.End;
```
----

**Given:** a pair of SnapshotPoint

**Get:** SnapshotSpan between them
```C#
var span = new SnapshotSpan(startPoint,  endPoint);
```
----

**Given:** ITextBuffer buffer, IClassifierAggregatorService classifierAggregatorService - obtain by MEF import

```C#
[Import]
internal IClassifierAggregatorService classifierAggregatorService = null;
```

**Get:** IClassifier of the text buffer
```C#
IClassifier m_classifier = classifierAggregatorService.GetClassifier(buffer);
```
----

**Given:** SnapshotSpan targetSpan, IClassifier m_classifier

**Get:** list of ClassificationSpan - within targetSpan, classified by a TokenTagger
```C#
var classificationSpans = m_classifier.GetClassificationSpans(targetSpan);
```
----

**Given:** ClassificationSpan classificationSpan

**Get:** ClassificationType of it
```C#
var classificationType = classificationSpan.ClassificationType;
```
----


**Given:** ClassificationType classificationType

**Get:** Classification name OR

**Check:** whether it is some certain type
```C#
string typeName = classificationType.Classification;
bool isComment = classificationType.IsOfType("comment");
```
----

