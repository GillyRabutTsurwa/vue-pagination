## Pagination functionality

- We created the Pagination component
- Ce composant acceptes ces trucs tant de props venant du composant App:
  - le numero des postes pour chaque page.
  - le numero des postes totaux (dans notre cas, c'est 100)
- lastly, page number takes the current page number upon click and emits an event to the parrent, which sets the current page number. The logic is rather complicated, so I will have to revise the code, but it works great.