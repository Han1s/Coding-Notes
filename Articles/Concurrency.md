
effective searchbar using **useTransition**
```tsx
import { useState, useTransition } from 'react';  
  
function SearchableList({ items }) {  
  const [inputValue, setInputValue] = useState('');  
  const [filterQuery, setFilterQuery] = useState('');  
  const = useTransition();  
  
  const handleInputChange = (e) => {  
    // 1. Urgent update: Update the input field immediately.  
    setInputValue(e.target.value);  
  
    // 2. Non-urgent update: Schedule the list filtering as a transition.  
    startTransition(() => {  
      setFilterQuery(e.target.value);  
    });  
  };  
  
  const filteredItems = items.filter(item =>  
    item.name.toLowerCase().includes(filterQuery.toLowerCase())  
  );  
  
  return (  
    <div>  
      <input  
        type="text"  
        value={inputValue}  
        onChange={handleInputChange}  
      />  
      {isPending && <p>Filtering...</p>}  
      <div style={{ opacity: isPending? 0.5 : 1 }}>  
        <ItemList items={filteredItems} />  
      </div>  
    </div>  
  );  
}
```

same searchbar with **useDefferedValue**
```tsx
import { useState, useDeferredValue } from 'react';  
  
function SearchableList({ items }) {  
  const [query, setQuery] = useState('');  
  const deferredQuery = useDeferredValue(query);  
  
  const filteredItems = items.filter(item =>  
    item.name.toLowerCase().includes(deferredQuery.toLowerCase())  
  );  
  
  const isStale = query!== deferredQuery;  
  
  return (  
    <div>  
      <input  
        type="text"  
        value={query}  
        onChange={e => setQuery(e.target.value)}  
      />  
      <div style={{ opacity: isStale? 0.5 : 1 }}>  
        <ItemList items={filteredItems} />  
      </div>  
    </div>  
  );  
}
```