# MoviesDatabase API Documentation Summary

## API Overview

MoviesDatabase is a comprehensive API providing up-to-date information on over **9 million** titles (movies, series, episodes) and **11 million** actors, crew, and cast members. It includes rich metadata such as YouTube trailer URLs, awards, full biographies, images, revenue, and extended cast. Recent titles are updated weekly, while ratings and episodes are updated daily.

Support the developer: [Buy Me a Coffee](https://www.buymeacoffee.com/SAdrian13)

---

## Version

Currently documented version: **v1** (unofficially inferred; versioning not explicitly stated)

---

## Available Endpoints

### Titles

- **GET /titles**  
  Returns an array of titles with optional filters and sorting.

- **GET /x/titles-by-ids**  
  Returns titles based on a provided array of IMDb IDs.

- **GET /titles/{id}**  
  Returns detailed info for a specific title by IMDb ID.

- **GET /titles/{id}/ratings**  
  Returns rating and number of votes for a title.

- **GET /titles/series/{id}**  
  Lists episodes by series ID.

- **GET /titles/seasons/{id}**  
  Returns number of seasons for a series.

- **GET /titles/series/{id}/{season}**  
  Lists episodes in a specific season.

- **GET /titles/episode/{id}**  
  Returns details of an episode.

- **GET /titles/x/upcoming**  
  Returns upcoming titles.

### Search

- **GET /titles/search/keyword/{keyword}**  
  Search titles by keyword.

- **GET /titles/search/title/{title}**  
  Search by title or partial title.

- **GET /titles/search/akas/{aka}**  
  Search by alternative known title (exact match, case sensitive).

### Actors

- **GET /actors**  
  Returns a list of actors with pagination.

- **GET /actors/{id}**  
  Returns detailed actor information by IMDb ID.

### Utils

- **GET /title/utils/titleType**  
  Returns title types.

- **GET /title/utils/genres**  
  Returns genre options.

- **GET /title/utils/lists**  
  Lists available predefined title lists (e.g. top rated).

---

## Request and Response Format

- All endpoints return JSON objects.
- Successful responses wrap data in a `results` key.
- Paged responses also include `page`, `next`, and `entries` keys.

### Example Request

```http
GET /titles/tt0000270?info=base_info
```

Example Response

```json
{
  "results": {
    "id": "tt0000270",
    "titleText": { "text": "Example Movie" },
    "ratingsSummary": { "averageRating": 6.5, "numVotes": 1631 }
    // ... more fields
  }
}
```

---

## Authentication

- No authentication key is explicitly required in the documentation.

- All query parameters are optional.

---

## Error Handling

- 404 Not Found: Invalid or unknown resource.

- Empty results: When filters return no matches.

- Proper error handling is recommended by checking results existence and structure.

## Usage Limits and Best Practices

- **Rate Limits:** Not documented, but keep requests under 1 per second to avoid rate limiting.

- **Pagination:** Use limit (max 50) and page to manage large result sets.

- **Info Query:** Use info to limit the amount of data returned (e.g., mini_info, rating, awards).

- **List Query:** When using the list parameter (e.g., top_rated_250), only 50 results are returned per request. Use pagination to access the rest.

- GET /titles?list=top_rated_250&limit=50&page=2

- Filter by Field: Use optional filters like titleType, startYear, endYear, genre, and sort for refined results.

- Use Utils: Call /title/utils/lists, /title/utils/titleType, and /title/utils/genres for up-to-date filtering options
