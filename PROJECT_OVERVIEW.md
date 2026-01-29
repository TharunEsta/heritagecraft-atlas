# Heritage Atlas - Project Overview

## Architecture

### System Design

```
┌─────────────────┐         ┌─────────────────┐         ┌─────────────────┐
│   React Frontend │ ◄─────► │  FastAPI Backend │ ◄─────► │    MongoDB      │
│   (Vercel)       │  HTTP   │    (Render)     │  Driver │   (Atlas/Local) │
└─────────────────┘         └─────────────────┘         └─────────────────┘
```

### Data Flow

1. **Product Upload Flow:**
   - Artisan fills form → Frontend sends POST request → Backend validates → MongoDB stores with GI metadata

2. **Product Discovery Flow:**
   - User selects region/GI tag → Frontend requests filtered data → Backend uses aggregation pipeline → Returns grouped results → Frontend displays on map/list

3. **Map Exploration Flow:**
   - User views map → Backend provides region data with coordinates → Frontend renders markers → User clicks marker → Shows region products

## Key Features Implementation

### 1. MongoDB Aggregation Pipelines

The backend uses several aggregation pipelines for efficient data processing:

**Region-Based Grouping:**
```python
pipeline = [
    {"$match": {"is_active": True}},
    {
        "$group": {
            "_id": "$region",
            "products": {"$push": {...}},
            "count": {"$sum": 1},
            "gi_tags": {"$addToSet": "$gi_tag"}
        }
    }
]
```

**Benefits:**
- Single query returns grouped data
- Reduces database round trips
- Efficient for map rendering
- Scales well with large datasets

### 2. Map-Centric UI

- Uses React Leaflet for interactive maps
- Markers positioned by region coordinates
- Popups show region statistics
- Sidebar lists all regions with product counts
- Click region to center map and show products

### 3. Region-Based Filtering

- Products stored with `region` and `gi_tag` fields
- Aggregation groups by these fields
- Frontend filters can combine multiple criteria
- Fast filtering using MongoDB indexes

### 4. Cultural Storytelling

- Each product includes `cultural_story` field
- Stories displayed on product detail pages
- Helps users understand heritage and traditions
- Encourages cultural appreciation

## API Endpoints

### Product Management
- `GET /api/products` - List products (with filters)
- `GET /api/products/{id}` - Get single product
- `POST /api/products` - Create product
- `GET /api/products/by-region` - Group by region
- `GET /api/products/by-gi-tag` - Group by GI tag

### Discovery
- `GET /api/regions` - All regions with stats
- `GET /api/gi-tags` - All GI tags with stats
- `GET /api/stats` - Platform statistics

## Database Schema

### Products Collection
```javascript
{
  _id: ObjectId,
  name: String,
  description: String,
  gi_tag: String,           // e.g., "Kondapalli", "Kalamkari"
  region: String,           // e.g., "Andhra Pradesh"
  artisan_name: String,
  artisan_contact: String,
  price: Number,
  category: String,
  image_url: String,
  location: {
    latitude: Number,
    longitude: Number
  },
  cultural_story: String,
  created_at: DateTime,
  updated_at: DateTime,
  is_active: Boolean
}
```

### Indexes (Recommended)
- `{region: 1}` - For region-based queries
- `{gi_tag: 1}` - For GI tag filtering
- `{is_active: 1}` - For active product filtering
- `{location: "2dsphere"}` - For geospatial queries (future)

## Frontend Components

### Pages
- **Home** - Dashboard with statistics and features
- **Products** - List view with filters
- **ProductDetail** - Single product view with cultural story
- **MapView** - Interactive map with region markers
- **UploadProduct** - Form for artisan product upload
- **About** - Platform information

### Key Components
- **Header** - Navigation bar
- **Map** - Leaflet map with markers
- **ProductCard** - Reusable product display
- **Filters** - Region/GI tag/Artisan filters

## Performance Optimizations

1. **Backend:**
   - Aggregation pipelines reduce queries
   - Indexed database fields
   - Pagination support
   - Efficient grouping operations

2. **Frontend:**
   - Component-based architecture
   - Lazy loading for images
   - Efficient state management
   - Optimized re-renders

## Deployment Strategy

### Frontend (Vercel)
- Static site generation
- Environment variables for API URL
- Automatic deployments from Git
- CDN distribution

### Backend (Render)
- Python runtime
- Environment variables for MongoDB
- Auto-scaling capability
- Health check endpoints

## Future Enhancements

1. **E-commerce Integration:**
   - Payment gateway integration
   - Shopping cart functionality
   - Order management

2. **Advanced Features:**
   - User authentication
   - Artisan profiles
   - Product reviews and ratings
   - Search functionality
   - Image upload (currently URL-based)

3. **Analytics:**
   - Product view tracking
   - Region popularity metrics
   - Artisan performance dashboards

4. **Mobile App:**
   - React Native version
   - Offline capability
   - Push notifications

## Security Considerations

1. **Input Validation:**
   - Form validation on frontend
   - Server-side validation in FastAPI
   - MongoDB injection prevention

2. **CORS Configuration:**
   - Restricted to frontend domain
   - Credentials handling

3. **Data Protection:**
   - Environment variables for secrets
   - Secure MongoDB connections
   - Input sanitization

## Testing Strategy

1. **Backend:**
   - Unit tests for aggregation pipelines
   - API endpoint tests
   - Database integration tests

2. **Frontend:**
   - Component tests
   - Integration tests
   - E2E tests for critical flows

## Monitoring & Logging

1. **Backend:**
   - Health check endpoint
   - Error logging
   - Request logging

2. **Frontend:**
   - Error boundaries
   - Console logging for debugging
   - Performance monitoring

## Scalability

The platform is designed to scale:

1. **Database:**
   - MongoDB sharding for large datasets
   - Read replicas for query distribution
   - Index optimization

2. **Backend:**
   - Horizontal scaling on Render
   - Load balancing
   - Caching strategies

3. **Frontend:**
   - CDN distribution via Vercel
   - Code splitting
   - Lazy loading

## Contributing

To contribute:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

[Specify your license here]
