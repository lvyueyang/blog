``` typescript
function arrayGroup<T>(arr: T[], size: number): T[][] {
  const _arr = [];
  for (let i = 0, len = arr.length; i < len; i += size) {
    _arr.push(arr.slice(i, i + size));
  }
  return _arr;
}
```
