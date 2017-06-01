# Ruby Refactoring Notes

## Case statement

### Starting Version

```
def available_page_title
  title = ""
  case
  when content_for?(:page_title)
    title = content_for(:page_title)
  when !@page_title.nil?
    title = @page_title
  when I18n.exists?('page_title.default')
    title = t('page_title.default')
  end
  title
end
```

### Refactored Version

```
def available_page_title
  title = case
    when content_for?(:page_title)
      content_for(:page_title)
    when @page_title
      @page_title
    when I18n.exists?('page_title.default')
      t('page_title.default')
    else
      ''
  end
end
```
