
> https://wiki.dendron.so/notes/GelEQPZrSgr3CK9y10Nrg/

## 스키마 템플릿에 frontmatter로 `published: false` 넣기

templates.daily.md (또는 지정한 템플릿 노트)의 프론트매터에 넣으면 됩니다.

```yaml
---
published: false
---
```

```md
## Thoughts

## Grateful

## Tasks
```

그리고 스키마에서 이 템플릿을 연결:

```yaml
version: 1
schemas:
  - id: daily
    parent: root
    children:
      - pattern: journal
        children:
          - pattern: "[0-2][0-9][0-9][0-9]"
            children:
              - pattern: "[0-1][0-9]"
                children:
                  - pattern: "[0-3][0-9]"
                    template: templates.daily
```

## 알려진 버그: `config` 키는 복사 안 되지만, 일반 **frontmatter** 키(`published` 등)는 정상 복사됨
