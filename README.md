# Zustand-api

    import create from 'zustand';
    
    const useStore = create((set) => ({
      data: null,
      isLoading: false,
      error: null,
      fetchData: async () => {
        set({ isLoading: true, error: null });
        try {
          const response = await fetch('/api/data');
          const data = await response.json();
          set({ data, isLoading: false });
        } catch (error) {
          set({ error, isLoading: false });
        }
      },
    }));

## api

    import create from 'zustand';
    
    const useStore = create((set) => ({
      isLoading: false,
      error: null,
      postData: async (data) => {
        set({ isLoading: true, error: null });
        try {
          const response = await fetch('/api/data', {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json',
            },
            body: JSON.stringify(data),
          });
    
          if (!response.ok) {
            throw new Error('Failed to post data');
          }
    
          // Handle successful response if needed
          const responseData = await response.json();
          console.log('Post data response:', responseData);
    
          set({ isLoading: false });
        } catch (error) {
          set({ error: error.message, isLoading: false });
        }
      },
    }));
    
    export default useStore;
