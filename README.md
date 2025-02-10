```mermaid
graph TD

    A[Start: Business Finance Dashboard] --> B[Load Sales Register];

    subgraph "Customer Data"
        C[Import Customer Master] -->|Get customer info| D[Stage Customer Data];
        B --> D
        D -->|Merge with Sales| E[Enrich Sales Data];
    end

    subgraph "Product Data"
        F[Import Product Master] -->|Get product MRP| G[Stage Product Data];
        B --> G
        G -->|Merge with Sales| H[Enrich Sales Data];
    end

    subgraph "prod_f9 Data"
        H -->|Get sub-category & brand| I[prod_f9 Data];
        I -->|Merge with Sales| J[Enrich Sales Data];
    end

    subgraph "DPC Cost"
        K[Import DPC Cost] -->|Merge with Sales| L[Add DPC Cost to Sales];
        B --> L
    end

    subgraph "Logistics Cost"
        B -->|Extract Logistics Cost| M[Calculate Logistics Cost];
    end

    subgraph "Packaging Cost"
        N[Import Packaging Cost] -->|Merge with Sales| O[Add Packaging Cost to Sales];
        B --> O
    end

    subgraph "Rent & Storage Cost"
        P[Import Rent & Storage Cost] -->|Merge with Sales| Q[Add Rent & Storage Cost to Sales];
        B --> Q
    end

    %% --- MERGE ALL --- %%
    E & H & J & L & M & O & Q --> T{Merge all?};
    T -- Yes --> U[Create Final DataFrame];

    subgraph "ANP Spends"
        U --> R[Import ANP Spends];
        R -->|Capture marketing costs| S[ANP Spends Data];
    end

    %% --- FINAL STEPS --- %%
    subgraph "Final Data & Calculations"
        S -->|Combine & Calculate| V[Comprehensive Financials];
        V --> W[Pivot & Filter];
        W --> X[Calculate Metrics];
        X -->|Finalize| Y[Final Processed DataFrame];
        Y -->|Factor to convert Costs| Z[Calculate Factors];
        Z -->|Add Freight Data| A1[Import Freight Data];  
    end

    %% --- DASHBOARD --- %%
    A1 --> B1[Business Insights Dashboard];
    B1 --> C1[End];
