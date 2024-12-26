# Modern ELT Pipeline Project

A robust Extract, Load, Transform (ELT) pipeline built with modern data tools including Airbyte, Airflow, and dbt. This project demonstrates a production-ready ELT workflow using containerized services.

## 🏗️ Architecture

This project implements a modern ELT architecture with the following components:

- **Airbyte**: Handles data extraction and loading (E & L)
- **dbt**: Manages data transformations (T)
- **Airflow**: Orchestrates the entire pipeline
- **PostgreSQL**: Serves as both source and destination databases
- **Docker**: Containerizes all services for consistent deployment

## 🚀 Quick Start

### Prerequisites

- Docker and Docker Compose
- Git
- Python 3.8+

### Setup Instructions

1. Clone the repository:
   ```bash
   git clone <your-repository-url>
   cd ELT-project-dbt
   ```

2. Set up environment variables:
   ```bash
   cp .env.example .env
   # Edit .env with your configurations
   ```

3. Start the services:
   ```bash
   ./start.sh
   ```

4. Stop the services:
   ```bash
   ./stop.sh
   ```

### DBT Configuration

Create or update your dbt profile at `~/.dbt/profiles.yml`:

```yaml
dbt_project:
  outputs:
    dev:
      dbname: destination_db
      host: host.docker.internal
      pass: postgres
      port: 5434
      schema: public
      threads: 1
      type: postgres
      user: postgres
  target: dev
```

## 📁 Project Structure

```
ELT-project-dbt/
├── airbyte/          # Airbyte configuration and connections
├── airflow/          # Airflow DAGs and configurations
├── dbt_project/      # DBT transformations and models
├── elt_script/       # ELT pipeline scripts
├── source_db_init/   # Initial database setup scripts
├── docker-compose.yaml
├── DockerFile
├── elt.sh           # Main ELT execution script
├── start.sh         # Service startup script
└── stop.sh          # Service shutdown script
```

## 🔧 Components

### Airbyte
- Manages data source connections
- Handles data extraction and loading
- Configurable through web UI at `localhost:8000`

### Airflow
- Orchestrates the entire ELT pipeline
- Manages task dependencies and scheduling
- Access the UI at `localhost:8080`

### DBT
- Handles data transformations
- Maintains data modeling
- Ensures data quality through tests

## 📊 Data Flow

1. Source data is extracted from PostgreSQL using Airbyte
2. Data is loaded into the destination database
3. DBT performs transformations on the loaded data
4. Airflow orchestrates the entire process

## 🛠️ Development

### Adding New Data Sources
1. Configure new source in Airbyte UI
2. Update corresponding connection settings
3. Modify dbt models as needed

### Creating New Transformations
1. Add new models in `dbt_project/models/`
2. Update `schema.yml` with model configurations
3. Run `dbt run` to test transformations

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Troubleshooting

Common issues and solutions:

- **Connection Issues**: Ensure all services are running with `docker ps`
- **Database Errors**: Check PostgreSQL logs in Docker
- **Transformation Failures**: Verify dbt models and run `dbt debug`

## 📚 Additional Resources

- [Airbyte Documentation](https://docs.airbyte.io/)
- [Apache Airflow Documentation](https://airflow.apache.org/docs/)
- [dbt Documentation](https://docs.getdbt.com/)

## 📋 TODO: Sakila Database Implementation

### Phase 1: Source Data Setup
- [ ] Set up Sakila sample database in source PostgreSQL
  - [ ] Import base tables and relationships
  - [ ] Verify data integrity and completeness
  - [ ] Configure proper indexing for performance

### Phase 2: Data Warehouse Design
1. Star Schema Implementation
   - [ ] Design fact tables
     - [ ] Rental facts (rental_id, customer_id, staff_id, inventory_id, dates, amounts)
     - [ ] Payment facts (payment_id, customer_id, staff_id, rental_id, amount, date)
   - [ ] Create dimension tables
     - [ ] Customer dimension (demographics, addresses)
     - [ ] Film dimension (categories, ratings, length)
     - [ ] Store dimension (locations, staff)
     - [ ] Time dimension (date hierarchies)

2. Snowflake Schema Extension
   - [ ] Normalize dimension tables
     - [ ] Split address into city, country hierarchies
     - [ ] Separate film categories and actors
     - [ ] Create language and rating dimensions

### Phase 3: DBT Transformations
- [ ] Create base models for initial data load
- [ ] Implement staging models
  - [ ] Customer staging
  - [ ] Film staging
  - [ ] Rental staging
  - [ ] Payment staging
- [ ] Develop mart models
  - [ ] Customer analytics mart
  - [ ] Film performance mart
  - [ ] Revenue analysis mart
  - [ ] Store performance mart
- [ ] Add data tests and documentation
  - [ ] Schema tests
  - [ ] Data quality tests
  - [ ] Business logic tests

### Phase 4: Airbyte Configuration
- [ ] Set up source connectors for Sakila database
- [ ] Configure destination connectors
- [ ] Define replication schedules
- [ ] Implement incremental sync strategies

### Phase 5: Airflow Orchestration
- [ ] Create DAG for initial load
- [ ] Implement incremental load DAGs
- [ ] Set up transformation scheduling
- [ ] Add monitoring and alerting

### Phase 6: Analytics & Dashboards
1. Tableau Dashboard Development
   - [ ] Revenue Analysis Dashboard
     - [ ] Daily/Monthly/Yearly revenue trends
     - [ ] Revenue by store location
     - [ ] Top performing films
     - [ ] Customer segments analysis
   
   - [ ] Inventory Performance Dashboard
     - [ ] Film category performance
     - [ ] Stock turnover rates
     - [ ] Rental duration analysis
     - [ ] Late returns tracking
   
   - [ ] Customer Insights Dashboard
     - [ ] Customer lifetime value
     - [ ] Rental frequency patterns
     - [ ] Geographic distribution
     - [ ] Payment behavior analysis

2. KPI Monitoring
   - [ ] Set up core business metrics
     - [ ] Revenue metrics
     - [ ] Customer metrics
     - [ ] Inventory metrics
   - [ ] Create KPI tracking dashboards
   - [ ] Implement alerts for metric thresholds

### Phase 7: Documentation & Handover
- [ ] Document data lineage
- [ ] Create data dictionary
- [ ] Prepare user guides for dashboards
- [ ] Document maintenance procedures

### Phase 8: Testing & Optimization
- [ ] Performance testing
- [ ] Query optimization
- [ ] Dashboard response time optimization
- [ ] User acceptance testing

## Expected Outcomes
1. A fully functional data warehouse with both star and snowflake schemas
2. Automated ELT pipeline with monitoring
3. Interactive Tableau dashboards for business insights
4. Comprehensive documentation and maintenance guides