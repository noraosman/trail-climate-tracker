# Trail Climate Tracker - Project Specification Document

**Project Name:** Trail Climate Tracker  
**Student:** Nora Osmanova  
**Institution:** University of Washington Bothell  
**Start Date:** November 9, 2025  
**Estimated Duration:** 10-12 weeks  

---

## Table of Contents
1. [Project Overview](#project-overview)
2. [Functional Requirements](#functional-requirements)
3. [Non-Functional Requirements](#non-functional-requirements)
4. [Technical Requirements](#technical-requirements)
5. [System Architecture](#system-architecture)
6. [Data Requirements](#data-requirements)
7. [User Interface Requirements](#user-interface-requirements)
8. [Testing Requirements](#testing-requirements)
9. [Development Milestones](#development-milestones)
10. [Resources Needed](#resources-needed)
11. [Deliverables](#deliverables)
12. [Success Criteria](#success-criteria)
13. [Risk Mitigation](#risk-mitigation)
14. [Appendices](#appendices)

---

## 1. PROJECT OVERVIEW

### 1.1 Project Description
A desktop/web application that integrates multiple environmental data APIs to provide hikers and outdoor enthusiasts with climate impact analysis for Pacific Northwest trails. The system will aggregate historical and current climate data, perform trend analysis, and visualize changes over time to raise awareness about climate impacts on outdoor recreation areas.

### 1.2 Project Goals
- Integrate at least 3 external REST APIs to fetch environmental data
- Implement object-oriented design principles throughout the system architecture
- Provide meaningful climate trend analysis for at least 10 Pacific Northwest trails
- Create data visualizations that clearly communicate climate changes over time
- Build a complete, deployable application suitable for portfolio demonstration

### 1.3 Target Users
- Pacific Northwest hikers and outdoor enthusiasts
- Environmental awareness advocates
- Outdoor recreation planners
- Climate-conscious trail users

### 1.4 Learning Objectives
- Master API integration and HTTP requests
- Practice object-oriented programming in Python
- Develop data analysis and visualization skills
- Build a complete project from design to deployment
- Create portfolio-quality work

---

## 2. FUNCTIONAL REQUIREMENTS

### 2.1 Core Features (Must Have - MVP)

#### FR-1: Trail Data Management
- System shall store information for at least 10 trails including:
  - Trail name
  - Geographic coordinates (latitude/longitude)
  - Elevation
  - Region/park name
  - Trail difficulty level
- System shall allow users to search trails by name or region
- System shall display basic trail information

#### FR-2: Climate Data Integration
- System shall integrate with NASA Earth Observation API to fetch:
  - Historical temperature data (minimum 5-year span)
  - Satellite imagery for specific trail locations
- System shall integrate with USGS Water Services API to fetch:
  - Stream flow data for trails near waterways
  - Water level measurements
- System shall integrate with OpenWeatherMap API to fetch:
  - Current weather conditions
  - 7-day forecast for trail locations
- System shall cache API responses to minimize redundant requests
- System shall handle API rate limits gracefully

#### FR-3: Climate Analysis
- System shall calculate temperature trends over time:
  - Average annual temperature
  - Seasonal temperature variations
  - Year-over-year temperature change
- System shall identify significant climate anomalies (e.g., unusually warm years)
- System shall compare current conditions to historical averages
- System shall generate a "climate impact score" for each trail

#### FR-4: Data Visualization
- System shall generate line charts showing temperature trends over time
- System shall create comparison visualizations (e.g., current year vs. historical average)
- System shall display satellite imagery comparisons (if available)
- System shall use color coding to indicate severity of climate changes
- All visualizations shall include proper labels, legends, and titles

#### FR-5: User Interface
- System shall provide a simple interface to:
  - Select a trail from a list
  - View trail information and current conditions
  - Display climate analysis results
  - Show data visualizations
- Interface can be command-line, desktop GUI, or web-based (student's choice)

### 2.2 Extended Features (Nice to Have - Post-MVP)

#### FR-6: Trail Condition Alerts
- System shall identify trails affected by:
  - Wildfire risk (based on temperature/drought data)
  - Flooding risk (based on precipitation/water level data)
  - Extreme weather conditions
- System shall display alert badges on affected trails

#### FR-7: Carbon Footprint Calculator
- System shall calculate estimated carbon footprint for:
  - Driving to trailhead
  - Alternative transportation options
- System shall compare carbon costs across different trails

#### FR-8: Data Export
- System shall allow users to export:
  - Climate analysis reports (PDF or CSV)
  - Visualization images (PNG)
  - Raw data for further analysis

#### FR-9: User Favorites
- System shall allow users to save favorite trails
- System shall provide quick access to saved trails
- System shall persist favorites between sessions

---

## 3. NON-FUNCTIONAL REQUIREMENTS

### 3.1 Performance Requirements
- **NFR-1**: API requests shall complete within 5 seconds under normal network conditions
- **NFR-2**: Application shall handle at least 50 trails without performance degradation
- **NFR-3**: Data visualizations shall render within 2 seconds
- **NFR-4**: System shall cache API responses for 24 hours to reduce load times

### 3.2 Reliability Requirements
- **NFR-5**: System shall handle API failures gracefully with informative error messages
- **NFR-6**: System shall validate all API responses before processing
- **NFR-7**: System shall continue functioning if one API service is unavailable (degrade gracefully)

### 3.3 Maintainability Requirements
- **NFR-8**: Code shall follow PEP 8 style guidelines (Python)
- **NFR-9**: All classes shall have clear docstrings explaining purpose and usage
- **NFR-10**: System architecture shall use OOP principles (inheritance, encapsulation, polymorphism)
- **NFR-11**: Configuration (API keys, settings) shall be externalized from code
- **NFR-12**: Code shall be modular to easily add new data sources

### 3.4 Usability Requirements
- **NFR-13**: Error messages shall be clear and actionable for users
- **NFR-14**: Visualizations shall be intuitive and require no technical knowledge to interpret
- **NFR-15**: Interface shall provide loading indicators for long-running operations

### 3.5 Security Requirements
- **NFR-16**: API keys shall NEVER be committed to version control
- **NFR-17**: User input shall be validated to prevent injection attacks
- **NFR-18**: System shall use HTTPS for all API communications

---

## 4. TECHNICAL REQUIREMENTS

### 4.1 Programming Language
- **Primary Language**: Python 3.9 or higher

### 4.2 Required Libraries/Frameworks
```
# Core libraries
requests==2.31.0          # HTTP requests for API calls
python-dotenv==1.0.0      # Environment variable management
pytest==7.4.0             # Unit testing

# Data processing
numpy==1.24.3             # Numerical computations
pandas==2.0.3             # Data manipulation and analysis

# Visualization
matplotlib==3.7.2         # Static visualizations
plotly==5.15.0            # Interactive visualizations (optional)

# Web framework (if building web app)
flask==2.3.3              # Lightweight web framework
OR
tkinter                   # Desktop GUI (included with Python)

# Additional utilities
pytz==2023.3              # Timezone handling
geopy==2.3.0              # Geographic calculations
```

### 4.3 Development Tools
- **Version Control**: Git + GitHub
- **IDE**: PyCharm, VS Code, or preferred Python IDE
- **Testing**: pytest for unit tests
- **Environment Management**: venv or conda
- **Documentation**: Markdown for README and docs

### 4.4 APIs Required

#### API 1: NASA Earth Observation (POWER Project)
- **Purpose**: Historical climate data (temperature, precipitation)
- **Endpoint**: https://power.larc.nasa.gov/api/temporal/daily/point
- **Authentication**: Free, no key required (or optional key for higher limits)
- **Rate Limit**: Generous (no official limit documented)
- **Cost**: Free
- **Documentation**: https://power.larc.nasa.gov/docs/

#### API 2: USGS Water Services
- **Purpose**: Real-time and historical water data
- **Endpoint**: https://waterservices.usgs.gov/rest/
- **Authentication**: None required
- **Rate Limit**: Reasonable use
- **Cost**: Free
- **Documentation**: https://waterservices.usgs.gov/rest/

#### API 3: OpenWeatherMap
- **Purpose**: Current weather and forecasts
- **Endpoint**: https://api.openweathermap.org/data/2.5/
- **Authentication**: API key required (free tier available)
- **Rate Limit**: 60 calls/minute (free tier)
- **Cost**: Free for up to 1,000 calls/day
- **Documentation**: https://openweathermap.org/api

#### API 4 (Optional): National Park Service
- **Purpose**: Trail and park information
- **Endpoint**: https://developer.nps.gov/api/v1/
- **Authentication**: API key required (free)
- **Rate Limit**: 1,000 calls/hour
- **Cost**: Free
- **Documentation**: https://www.nps.gov/subjects/developer/api-documentation.htm

---

## 5. SYSTEM ARCHITECTURE

### 5.1 Required Classes/Modules

#### Module 1: Data Models
**You will design classes to represent:**
- Trail information (name, location, characteristics)
- Climate data points (measurements from APIs)

**Design considerations:**
- What attributes does a trail need?
- What attributes does a climate measurement need?
- What operations might you need to perform on this data?
- How will you validate data?
- How will you convert between formats (e.g., to/from JSON)?

*Specific design decisions are left to you - this is part of your Week 1 design phase.*

#### Module 2: API Integration
**You will design classes to fetch data from different APIs:**
- A base class that all API fetchers inherit from
- Specific fetchers for each API (NASA, USGS, OpenWeatherMap)

**Design considerations:**
- What do ALL API fetchers have in common? (Put this in the base class)
- What's unique to each specific API? (Put this in child classes)
- How will you handle errors?
- How will you parse different JSON response formats?
- How will you implement caching?
- How will you handle rate limits?

**This demonstrates inheritance and polymorphism in OOP.**

*Specific design decisions are left to you - this is part of your Week 1 design phase.*

#### Module 3: Data Processing
**You will design classes to analyze climate data:**
- A class that performs climate analysis and calculations
- A class that manages data caching

**Design considerations for Climate Analyzer:**
- What inputs does it need? (What data?)
- What calculations will you perform? (Temperature trends, averages, anomalies?)
- What outputs will it produce? (Analysis results, scores?)
- How will you handle missing or incomplete data?

**Design considerations for Data Cache:**
- How will you store cached data?
- How will you know if cache is still valid?
- When should cache expire?
- How will you retrieve cached data?

*Specific design decisions are left to you - this is part of your Week 1 design phase.*

#### Module 4: Visualization
**You will design a class to create data visualizations:**

**Design considerations:**
- What types of charts will you create? (Line charts, bar charts, comparisons?)
- What library will you use? (Matplotlib, Plotly, both?)
- How will you handle chart creation? (One method per chart type? One flexible method?)
- How will you save visualizations?
- How will you display them to users?
- What customization options do you need? (Colors, labels, titles?)

*Specific design decisions are left to you - this is part of your Week 1 design phase.*

#### Module 5: Application Controller
**You will design a main application class that coordinates everything:**

**Design considerations:**
- How will you initialize all the components?
- How will you handle user input?
- How will you coordinate between different modules? (fetchers → analyzer → visualizer)
- What's the main workflow/process flow?
- How will you handle errors at the application level?

**This is the "orchestrator" that brings all your classes together.**

*Specific design decisions are left to you - this is part of your Week 1 design phase.*

### 5.2 Data Flow
1. User selects a trail → TrailClimateApp
2. App retrieves trail coordinates → TrailData
3. App requests climate data → ClimateDataFetcher subclasses
4. Fetchers retrieve data from APIs → parse and return
5. App analyzes data → ClimateAnalyzer
6. App generates visualizations → DataVisualizer
7. Results displayed to user

### 5.3 File Structure
```
trail-climate-tracker/
├── README.md
├── requirements.txt
├── .env.example
├── .gitignore
├── src/
│   ├── __init__.py
│   ├── main.py
│   ├── models/
│   │   ├── __init__.py
│   │   ├── trail_data.py
│   │   ├── climate_data.py
│   ├── api/
│   │   ├── __init__.py
│   │   ├── base_fetcher.py
│   │   ├── nasa_fetcher.py
│   │   ├── usgs_fetcher.py
│   │   ├── weather_fetcher.py
│   ├── analysis/
│   │   ├── __init__.py
│   │   ├── climate_analyzer.py
│   │   ├── data_cache.py
│   ├── visualization/
│   │   ├── __init__.py
│   │   ├── visualizer.py
│   ├── ui/
│   │   ├── __init__.py
│   │   ├── app.py
│   ├── config/
│   │   ├── __init__.py
│   │   ├── settings.py
├── data/
│   ├── trails.json
│   ├── cache/
├── tests/
│   ├── __init__.py
│   ├── test_trail_data.py
│   ├── test_fetchers.py
│   ├── test_analyzer.py
├── docs/
│   ├── architecture.md
│   ├── api_guide.md
│   ├── user_guide.md
└── output/
    ├── visualizations/
    ├── reports/
```

---

## 6. DATA REQUIREMENTS

### 6.1 Trail Database
**Initial dataset shall include 10 Pacific Northwest trails:**

1. **Mt. Rainier National Park**
   - Skyline Trail (46.7869° N, 121.7369° W)
   - Wonderland Trail section (46.8523° N, 121.7603° W)

2. **Olympic National Park**
   - Hoh River Trail (47.8607° N, 123.9351° W)
   - Hurricane Ridge (47.9698° N, 123.4968° W)

3. **North Cascades**
   - Cascade Pass (48.4754° N, 121.0736° W)
   - Sahale Arm (48.5043° N, 121.0405° W)

4. **Alpine Lakes Wilderness**
   - Colchuck Lake (47.4772° N, 120.8348° W)
   - Enchantment Lakes (47.4773° N, 120.8003° W)

5. **Columbia River Gorge**
   - Eagle Creek Trail (45.6368° N, 121.9198° W)

6. **Mount St. Helens**
   - Monitor Ridge (46.1914° N, 122.1956° W)

### 6.2 Data Format (JSON)
```json
{
  "trails": [
    {
      "trail_id": 1,
      "name": "Skyline Trail",
      "park": "Mt. Rainier National Park",
      "region": "Washington",
      "latitude": 46.7869,
      "longitude": -121.7369,
      "elevation_ft": 5400,
      "difficulty": "moderate",
      "length_miles": 5.5,
      "has_water_source": true
    }
  ]
}
```

### 6.3 Climate Data Points
**For each trail, fetch the following data:**
- Daily temperature (min, max, average) for past 5-10 years
- Precipitation data
- Stream flow (if near water source)
- Current weather conditions

### 6.4 Cache Requirements
- Cache API responses for 24 hours
- Store cache in local JSON files or SQLite database
- Include cache timestamp and expiration logic

---

## 7. USER INTERFACE REQUIREMENTS

### 7.1 Interface Options (Choose One)

#### Option A: Command Line Interface
```
=== Trail Climate Tracker ===

Available trails:
1. Skyline Trail (Mt. Rainier)
2. Hoh River Trail (Olympic NP)
3. Cascade Pass (North Cascades)
...

Select trail number: 1

Loading climate data...
Analyzing trends...

--- Skyline Trail Climate Report ---
Location: Mt. Rainier National Park
Elevation: 5,400 ft
Coordinates: 46.7869°N, 121.7369°W

Current Conditions:
  Temperature: 52°F
  Conditions: Partly Cloudy
  Wind: 8 mph NW

Climate Trends (2015-2025):
  Avg Annual Temp: 42°F (↑ 2.3°F from baseline)
  Warmest Year: 2024 (44.5°F)
  Coldest Year: 2017 (39.1°F)
  
Climate Impact Score: 6.5/10 (Moderate)

[Press V to view visualizations]
[Press E to export report]
[Press B to go back]
```

#### Option B: Desktop GUI (tkinter)
- Left panel: List of trails
- Center panel: Trail details and climate data
- Right panel: Visualizations
- Bottom panel: Status bar and action buttons

#### Option C: Web Application (Flask)
- Homepage with trail search
- Trail detail page with climate analysis
- Interactive charts using Plotly
- Responsive design

### 7.2 Required Screens/Views
1. **Trail Selection Screen**: Display list of available trails
2. **Trail Detail Screen**: Show trail info and current conditions
3. **Climate Analysis Screen**: Display trends and analysis
4. **Visualization Screen**: Show charts and graphs
5. **Error Screen**: Display friendly error messages

---

## 8. TESTING REQUIREMENTS

### 8.1 Unit Tests Required
- Test TrailData model validation
- Test each API fetcher's parse_response() method
- Test ClimateAnalyzer calculations
- Test DataCache functionality
- Test error handling for API failures

### 8.2 Integration Tests
- Test complete data flow from API to visualization
- Test multiple API calls in sequence
- Test cache behavior

### 8.3 Test Coverage Goal
- Minimum 70% code coverage
- 100% coverage for critical data processing functions

### 8.4 Sample Test Cases
```python
# Example test structure
def test_trail_data_validation():
    """Test that TrailData validates coordinates correctly"""
    pass

def test_nasa_api_fetch():
    """Test NASA API fetcher returns expected data format"""
    pass

def test_temperature_trend_calculation():
    """Test that temperature trends are calculated correctly"""
    pass

def test_api_rate_limit_handling():
    """Test that system handles rate limit errors gracefully"""
    pass
```

---

## 9. DEVELOPMENT MILESTONES

### Phase 1: Setup & Foundation (Week 1-2) ✅ COMPLETED
- [x] Set up project structure and Git repository
- [x] Obtain all API keys
- [x] Create trail database (trails.json)
- [ ] Design UML class diagrams
- [ ] Implement TrailData model
- [ ] Set up testing framework

**Deliverable**: Project structure with basic models and test framework

### Phase 2: API Integration (Week 3-4)
- [ ] Implement ClimateDataFetcher base class
- [ ] Implement NASADataFetcher
- [ ] Implement USGSDataFetcher
- [ ] Implement WeatherAPIFetcher
- [ ] Test each fetcher independently
- [ ] Implement DataCache

**Deliverable**: Working API integration layer with all three APIs

### Phase 3: Data Analysis (Week 5-6)
- [ ] Implement ClimateAnalyzer
- [ ] Add temperature trend calculations
- [ ] Add anomaly detection
- [ ] Add climate impact scoring
- [ ] Write unit tests for analysis functions

**Deliverable**: Complete data analysis module with tests

### Phase 4: Visualization (Week 7)
- [ ] Implement DataVisualizer
- [ ] Create temperature trend charts
- [ ] Create comparison visualizations
- [ ] Test visualization generation

**Deliverable**: Working visualization module

### Phase 5: User Interface (Week 8-9)
- [ ] Implement chosen UI (CLI/GUI/Web)
- [ ] Integrate all modules
- [ ] Add error handling and user feedback
- [ ] Test complete user workflows

**Deliverable**: Functional application with UI

### Phase 6: Polish & Documentation (Week 10)
- [ ] Write comprehensive README
- [ ] Add code comments and docstrings
- [ ] Create user guide
- [ ] Add extended features (if time permits)
- [ ] Final testing and bug fixes

**Deliverable**: Complete, documented, portfolio-ready project

---

## 10. RESOURCES NEEDED

### 10.1 API Keys to Obtain

#### 1. OpenWeatherMap API Key ✅ OBTAINED
- Website: https://openweathermap.org/api
- Steps:
  1. Create free account
  2. Navigate to API keys section
  3. Generate new key
  4. Copy key to .env file
- Activation time: Instant to 2 hours
- Free tier: 1,000 calls/day, 60 calls/minute

#### 2. National Park Service API Key (Optional)
- Website: https://www.nps.gov/subjects/developer/get-started.htm
- Steps:
  1. Fill out request form
  2. Receive key via email
  3. Copy key to .env file
- Activation time: Instant
- Free tier: 1,000 calls/hour

#### 3. NASA POWER API
- No key required OR optional registration for higher limits
- Website: https://power.larc.nasa.gov/docs/
- If registering: follow signup process on NASA website

### 10.2 Learning Resources

#### API Basics:
- "Working with APIs in Python" - Real Python tutorial
- "Python Requests Library Documentation" - https://requests.readthedocs.io/
- YouTube: "REST APIs explained in 5 minutes"

#### Data Analysis:
- "NumPy Basics" - NumPy documentation quickstart
- "Pandas Tutorial" - pandas official documentation

#### Visualization:
- Matplotlib tutorials
- "Plotly Python Tutorial" for interactive charts
- "5 Quick and Easy Data Visualizations in Python"

#### OOP in Python:
- "Object-Oriented Programming in Python" - Real Python
- "Python Abstract Base Classes" - Python ABC documentation

#### Flask (if building web app):
- "Flask Mega-Tutorial" by Miguel Grinberg
- Flask documentation: https://flask.palletsprojects.com/

### 10.3 Reference Documentation
- Python Requests: https://requests.readthedocs.io/
- Matplotlib: https://matplotlib.org/stable/tutorials/index.html
- NumPy: https://numpy.org/doc/stable/user/quickstart.html
- Pandas: https://pandas.pydata.org/docs/user_guide/index.html
- pytest: https://docs.pytest.org/

### 10.4 Development Environment Setup ✅ COMPLETED

**Required Software:**
- Python 3.9+ ✅
- Git ✅
- VS Code ✅
- pip (package installer) ✅

### 10.5 Pacific Northwest Trail Data Sources
- Washington Trails Association: https://www.wta.org/
- AllTrails: https://www.alltrails.com/
- National Park Service websites
- USGS Topo Maps

---

## 11. DELIVERABLES

### 11.1 Code Deliverables
1. Complete Python application with all required modules
2. Unit tests with >70% coverage
3. Sample trail database (trails.json)
4. Configuration files (.env.example)
5. Requirements.txt with all dependencies ✅ COMPLETED

### 11.2 Documentation Deliverables
1. **README.md** including:
   - Project description ✅ COMPLETED
   - Installation instructions
   - Usage examples
   - API key setup guide
   - Screenshots/examples
2. **Architecture documentation** (architecture.md)
3. **API integration guide** (api_guide.md)
4. **Code comments and docstrings** throughout

### 11.3 Visual Deliverables
1. At least 3 types of data visualizations
2. Screenshots of application in use
3. Sample output reports

### 11.4 Repository Deliverables
1. GitHub repository with:
   - Clear commit history ✅ IN PROGRESS
   - Organized file structure ✅ COMPLETED
   - .gitignore file ✅ COMPLETED
   - Professional README ✅ COMPLETED
   - MIT or similar open-source license

---

## 12. SUCCESS CRITERIA

### 12.1 Minimum Viable Product (MVP) Criteria
- ✅ Application successfully fetches data from 3 APIs
- ✅ Climate trends calculated for at least 10 trails
- ✅ At least 2 types of visualizations generated
- ✅ Error handling for API failures implemented
- ✅ Basic UI (CLI, GUI, or web) functional
- ✅ Code follows OOP principles with clear class hierarchy
- ✅ Unit tests written and passing
- ✅ Documentation complete and clear

### 12.2 Resume-Ready Criteria
- ✅ GitHub repository is public and well-organized
- ✅ README includes screenshots and clear instructions
- ✅ Code demonstrates strong OOP design
- ✅ Project shows API integration skills
- ✅ Data analysis and visualization capabilities evident
- ✅ Professional code quality (comments, formatting, naming)

### 12.3 Bonus Achievement Criteria
- ⭐ Added extended features (alerts, carbon calculator, etc.)
- ⭐ Deployed web application (if applicable)
- ⭐ Test coverage >80%
- ⭐ Integration with 4+ APIs
- ⭐ Interactive visualizations (Plotly)
- ⭐ Mobile-responsive design (if web app)

---

## 13. RISK MITIGATION

### 13.1 Technical Risks

#### Risk 1: API Rate Limiting
- **Impact**: High - could block development/testing
- **Probability**: Medium
- **Mitigation**: 
  - Implement caching from day 1 ✅
  - Use mock data for testing
  - Test with small datasets first
  - Space out API calls during development

#### Risk 2: API Reliability
- **Impact**: Medium - some APIs might be down temporarily
- **Probability**: Low
- **Mitigation**:
  - Implement graceful degradation
  - Build fallback mechanisms
  - Test error handling thoroughly
  - Don't rely on single API for critical features

#### Risk 3: Coordinate Data Accuracy
- **Impact**: Medium - wrong coordinates = wrong climate data
- **Probability**: Low
- **Mitigation**:
  - Verify all trail coordinates from multiple sources
  - Test with known locations first
  - Add validation for coordinate ranges

#### Risk 4: Scope Creep
- **Impact**: High - could prevent completion
- **Probability**: High (common for self-directed projects!)
- **Mitigation**:
  - Stick to MVP features first
  - Document "future features" list separately
  - Complete one phase before starting next
  - Remember: Done is better than perfect!

### 13.2 Timeline Risks

#### Risk 5: Underestimating complexity
- **Impact**: High - could extend timeline significantly
- **Probability**: Medium
- **Mitigation**:
  - Build buffer time into each phase
  - Start with simplest features
  - Get one API working completely before adding others
  - It's okay to take longer than 10 weeks!

---

## 14. APPENDICES

### Appendix A: Example API Response Formats

#### NASA POWER API Response
```json
{
  "parameters": {
    "T2M": {
      "20230101": 2.5,
      "20230102": 3.1,
      "20230103": 1.8
    }
  },
  "geometry": {
    "coordinates": [-121.7369, 46.7869]
  }
}
```

#### OpenWeatherMap Response
```json
{
  "coord": {"lon": -121.7369, "lat": 46.7869},
  "weather": [{"main": "Clouds", "description": "scattered clouds"}],
  "main": {
    "temp": 284.15,
    "feels_like": 282.34,
    "temp_min": 281.48,
    "temp_max": 286.71
  },
  "wind": {"speed": 3.6, "deg": 310}
}
```

#### USGS Water Services Response
```json
{
  "value": {
    "timeSeries": [{
      "variable": {
        "variableName": "Streamflow",
        "unit": {"unitCode": "ft3/s"}
      },
      "values": [{
        "value": [{
          "value": "1230",
          "dateTime": "2025-01-15T08:00:00"
        }]
      }]
    }]
  }
}
```

### Appendix B: Resume Bullet Points

**Once completed, add these to your resume:**

- "Designed and implemented object-oriented architecture for climate monitoring system integrating 3+ REST APIs (NASA, USGS, OpenWeatherMap)"

- "Built Python application to analyze 5+ years of historical temperature data across 10+ Pacific Northwest trails, identifying climate trends and anomalies"

- "Developed data visualization module using Matplotlib to generate comparative climate analysis charts and trend visualizations"

- "Implemented caching system and error handling to manage API rate limits and ensure system reliability"

- "Created sustainable technology solution raising climate awareness for outdoor recreation community"

### Appendix C: Git Best Practices

**Good Commit Messages:**
- "Add requirements.txt"
- "Implement TrailData model with validation"
- "Add NASA API fetcher with error handling"
- "Create temperature trend visualization"

**Bad Commit Messages:**
- "stuff"
- "changes"
- "asdfasdf"
- "fixed it"

**Commit Frequency:**
- Commit after completing each small task
- Push to GitHub at least daily
- Don't commit broken code to main branch

### Appendix D: .env.example Template

Create this file to show others what environment variables are needed:

```
# Trail Climate Tracker - Environment Variables
# Copy this file to .env and fill in your actual API keys

# OpenWeatherMap API Key
# Get yours at: https://openweathermap.org/api
OPENWEATHER_API_KEY=your_key_here

# NASA POWER API Key (Optional)
# Get yours at: https://power.larc.nasa.gov/
NASA_API_KEY=your_key_here

# National Park Service API Key (Optional)
# Get yours at: https://www.nps.gov/subjects/developer/get-started.htm
NPS_API_KEY=your_key_here
```

---

## DOCUMENT HISTORY

**Version 1.0** - November 9, 2025
- Initial specification created
- Day 1 tasks completed (setup, Git, venv, API key)
- Project structure established

**Future Updates:**
- Version 1.1 will include design decisions from Week 1
- Version 1.2 will include API integration details from Phase 2
- Final version will include lessons learned and retrospective

---

## CONTACT & SUPPORT

**Student:** Nora Osmanova  
**GitHub:** https://github.com/noraosman  
**LinkedIn:** https://www.linkedin.com/in/aosmanova/  
**Email:** aynura.osman@gmail.com  

**Project Repository:** https://github.com/noraosman/trail-climate-tracker

---

## NOTES

This specification document is a living document and will be updated as the project progresses. Keep this file as a reference throughout development.

**Remember:**
- Design first, code later
- Commit often, push daily
- Test as you go
- Document everything
- Ask for help when stuck
- Celebrate small wins!

**Good luck with your project! 🚀**

---

*End of Specification Document*
