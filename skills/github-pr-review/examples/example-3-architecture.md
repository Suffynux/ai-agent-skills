# Example 3: Architecture and Design Recommendations

## Scenario

A developer implements a caching layer for their API but does not account for potential issues in a distributed system. The feature works in development but would fail in production.

## Original Code Review

```typescript
// src/cache/user-cache.ts
class UserCache {
  private cache: Map<string, User> = new Map();
  private CACHE_TTL = 5 * 60 * 1000; // 5 minutes

  async getUser(userId: string): Promise<User | null> {
    // Check cache first
    if (this.cache.has(userId)) {
      const user = this.cache.get(userId)!;
      if (Date.now() - user.cachedAt < this.CACHE_TTL) {
        return user;
      }
      this.cache.delete(userId);
    }

    // Not in cache, fetch from database
    const user = await database.getUser(userId);
    
    // Store in cache
    if (user) {
      user.cachedAt = Date.now();
      this.cache.set(userId, user);
    }

    return user;
  }
}
```

## AI Agent Review

```
ARCHITECTURE REVIEW
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Overall: Good foundation, but needs work for production

WHAT IS GOOD:
- Clear cache TTL (5 minutes is reasonable)
- Clean implementation
- Good error handling

ISSUES FOUND:

ISSUE #1: Single-Server Cache Will Not Scale
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Severity: Medium (High for production)

Problem:
- Cache stored only in memory (Map)
- Not shared between servers
- Each server has its own cache
- Creates cache inconsistency

Example scenario:
1. Server A gets User ID: 123
2. Server A caches User data
3. User data is updated in database
4. Server B gets User ID: 123
5. Server A returns OLD cached data from Server A
6. Server B returns NEW data from database
7. User sees inconsistent data

Solution: Use distributed cache (Redis)

ISSUE #2: No Cache Invalidation Strategy
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Severity: High

Problem:
- When data is updated, cache is not invalidated
- Users see outdated data for up to 5 minutes
- Updates might appear not to work

Solution: Invalidate cache when data changes

ISSUE #3: No Handling of Cache Failures
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Severity: Medium

Problem:
- If caching fails, no fallback
- No error logging
- No monitoring

Solution: Add error handling and logging

RECOMMENDED ARCHITECTURE:

// Use distributed cache (Redis)
import Redis from 'redis';

class UserCache {
  private redis = new Redis();
  private CACHE_TTL = 5 * 60; // 5 minutes in seconds

  async getUser(userId: string): Promise<User | null> {
    try {
      // Check distributed cache
      const cached = await this.redis.get(`user:${userId}`);
      if (cached) {
        return JSON.parse(cached);
      }

      // Not in cache, fetch from database
      const user = await database.getUser(userId);
      
      // Store in distributed cache
      if (user) {
        await this.redis.setex(
          `user:${userId}`,
          this.CACHE_TTL,
          JSON.stringify(user)
        );
      }

      return user;
    } catch (error) {
      // Cache failure - fallback to database
      logger.error('Cache error', { error, userId });
      return database.getUser(userId);
    }
  }

  // NEW: Invalidate cache when user is updated
  async invalidateUser(userId: string): Promise<void> {
    try {
      await this.redis.del(`user:${userId}`);
    } catch (error) {
      logger.error('Cache invalidation error', { error, userId });
    }
  }
}

SCALABILITY COMPARISON:

Current Approach (In-Memory):
- Servers: 1 - Works
- Servers: 5 - Cache inconsistencies
- Servers: 100 - Complete failure

Recommended Approach (Redis):
- Servers: 1 - Works
- Servers: 5 - All consistent
- Servers: 100 - Scales perfectly

ADDITIONAL RECOMMENDATIONS:

1. Add cache hit/miss metrics
2. Monitor cache performance
3. Add circuit breaker for cache failures
4. Document cache invalidation strategy
5. Test with multiple servers

EFFORT: 2-4 hours to implement properly
IMPACT: Critical for production scalability
WORTH IT: Yes - Prevents major bugs at scale

NEXT STEPS:
1. Switch to distributed cache (Redis)
2. Add cache invalidation strategy
3. Add error handling
4. Add monitoring and metrics
5. Test with multiple server instances
6. Re-request review

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Developer's Response

The developer appreciated the architectural guidance:

> This is exactly the kind of feedback I needed. I was thinking about scaling later, but you are right - this would be a problem as soon as we run multiple instances. I will switch to Redis today.

## Implementation

The developer implemented the recommendations:
- Switched to Redis for distributed caching
- Added cache invalidation on data updates
- Added comprehensive error handling
- Added monitoring and metrics
- Tested with 5 server instances

## Lesson Learned

Architecture issues often do not appear in single-server development. AI code review helps identify scalability problems before they cause outages in production.

---

*Example Review: AI Agent Skills - GitHub PR Review Skill*