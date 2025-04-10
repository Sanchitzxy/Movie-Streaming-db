# Movie Streaming Platform Database

This is a comprehensive, production-ready database design for a Netflix-like streaming service. The database includes all essential components of a modern streaming platform including user management, content catalog, viewing history, recommendations, subscription management, and more.

## Database Overview

This database is designed to support a full-featured movie streaming platform with the following capabilities:

- User account and profile management (similar to Netflix's multi-profile system)
- Content catalog with movies and TV shows (including seasons and episodes)
- Personalized recommendations based on viewing history
- Subscription and payment management
- Device tracking and session management
- User interactions (watchlist, viewing history, ratings and reviews)
- Administrative functions for content and user management

## Entity Relationship Diagram

The database follows a normalized design with appropriate relationships between entities:

- Users can have multiple profiles
- Content (movies/TV shows) has many-to-many relationships with actors, directors, and genres
- TV shows have seasons, which have episodes
- Users can leave reviews and ratings for content
- Users have subscriptions and payment history
- Viewing history tracks what users watch and when

## Tables

1. **Users** - Account holders information
2. **Profiles** - Multiple profiles per user account
3. **Content** - Movies and TV shows metadata
4. **Seasons** - TV show seasons
5. **Episodes** - TV show episodes
6. **People** - Actors, directors, and other content creators
7. **Genres** - Content categories
8. **Content_Genres** - Many-to-many relationship between content and genres
9. **Content_People** - Many-to-many relationship between content and people with roles
10. **Viewing_History** - Tracks what users watch
11. **Watchlist_Items** - Users' saved content for later viewing
12. **Content_Reviews** - User ratings and reviews
13. **Subscription_Plans** - Available subscription tiers
14. **Subscriptions** - User subscriptions
15. **Payment_Transactions** - Payment history
16. **Devices** - User devices used for streaming
17. **Device_Sessions** - Login sessions on devices
18. **Content_Recommendations** - Content-based recommendations
19. **User_Recommendations** - User-specific recommendations
20. **Admins** - Administrative users for platform management

## Advanced Features

The database includes several advanced features:

- **Stored Procedures** for generating recommendations
- **Triggers** for automatically updating content ratings
- **Views** for popular and trending content
- **Functions** for personalized content, subscription statistics, and user activity metrics

## Implementation

The database is implemented in PostgreSQL but can be adapted to other RDBMS systems with minimal changes. The implementation includes:

1. Table creation with appropriate constraints and relationships
2. Sample data population
3. Indexes for performance optimization
4. Stored procedures and functions for common operations

## How to Use

### Setup Instructions

1. Install PostgreSQL if not already installed
2. Create a new database
3. Run the SQL scripts in the following order:
   - `movie_streaming_platform_db.sql` (main schema)
   - `movie_streaming_platform_db_part2.sql` (additional data)
   - `movie_streaming_platform_db_part3.sql` (stored procedures and functions)

```sql
-- Example commands to run the scripts
psql -U username -d database_name -f movie_streaming_platform_db.sql
psql -U username -d database_name -f movie_streaming_platform_db_part2.sql
psql -U username -d database_name -f movie_streaming_platform_db_part3.sql
```

### Using the Database

Once set up, you can use the database for:

- Building a streaming application backend
- Analyzing user viewing patterns
- Managing content catalog
- Processing subscriptions and payments
- Generating personalized recommendations

## Sample Queries

### Get User Profiles
```sql
SELECT * FROM profiles WHERE user_id = 1;
```

### Get Content with Genres
```sql
SELECT c.title, g.name 
FROM content c
JOIN content_genres cg ON c.content_id = cg.content_id
JOIN genres g ON cg.genre_id = g.genre_id
WHERE c.content_id = 1;
```

### Get Personalized Recommendations
```sql
SELECT * FROM get_personalized_content(1, 10);
```

### Get Subscription Statistics
```sql
SELECT * FROM get_subscription_stats();
```

### Get User Viewing History
```sql
SELECT vh.start_time, c.title, vh.percentage_watched
FROM viewing_history vh
LEFT JOIN content c ON vh.content_id = c.content_id
LEFT JOIN episodes e ON vh.episode_id = e.episode_id
LEFT JOIN seasons s ON e.season_id = s.season_id
LEFT JOIN content c2 ON s.content_id = c2.content_id
WHERE vh.profile_id = 1
ORDER BY vh.start_time DESC;
```

## Extensibility

This database design can be extended to include additional features such as:

- Content subtitles and multiple audio tracks
- User preferences for playback settings
- Social features (sharing, friends recommendations)
- More advanced recommendation algorithms
- Content licensing and regional availability
- Analytics for content performance and user engagement
