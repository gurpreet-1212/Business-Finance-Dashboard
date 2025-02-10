```mermaid
graph TD

    A[Start: Business Finance Dashboard] --> B[Load Sales Register Dataset];

    subgraph "Customer Data"
        B -->|Get customer attributes| C[Import Customer Master Data];
        C --> D[Stage Customer Data & Merge with Sales Register];
        D -->|Link customer details with sales| E[Create Merged Customer-Sales DataFrame];
    end

    subgraph "Product Data"
        B -->|Get product MRP| F[Import Product Master Data];
        F --> G[Extract Product Details];
        G -->|Add product metadata to transactions| H[Create Product Details DataFrame];
        H --> I[Merge Product Items with Base Dataset];
        I --> J[Add Category, Sub-category, and Brand Information];
        J -->|Enable category-wise sales & cost analysis| K[Create Categorized Sales DataFrame];
    end

    subgraph "Cost Metrics"
        K --> L[Extract Cost Metrics];
        L --> M[DPC Cost Calculation];
        M -->|Essential for cost analysis| N[Create Cost Analysis DataFrame];
        N --> O[Reset Logistics & Packaging Costs];
        O -->|Separate costs for accuracy| P[Create Cost Adjustments DataFrame];
    end

    subgraph "AMP Spends"
        P --> Q[Import AMP Spends Data];
        Q --> R[Merge AMP Spends for DPL Calculation];
        R -->|Capture marketing costs| S[Create AMP Spends DataFrame];
    end

    %% --- MERGE ALL DATAFRAMES --- %%
    E & K & P & S --> T{Merge all dataframes?};

    T -- Yes --> U[Create Final DataFrame];

    %% --- FINAL STEPS --- %%
    subgraph "Final Data & Calculations"
        U --> V[Combine data & calculate metrics];
        V --> W[Handle Nulls & Adjustments];
        W --> X[Create Final Business Finance DataFrame];
    end

    subgraph "Dashboard & Reporting"
        X --> Y[Final Financial & Business Insights Dashboard];
        Y --> Z[Generate Reports & Visualizations];
        Z --> A1[End: Dashboard Ready for Analysis];
    end
