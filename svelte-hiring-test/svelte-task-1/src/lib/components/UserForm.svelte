<script lang="ts">
    // TODO: Implement form state management
    // TODO: Implement form validation
    // TODO: Implement submit handler
    // TODO: Implement success state management
</script>

<div class="form-container">
    <form>
        <div class="form-group">
            <label for="firstName">First Name</label>
            <input
                id="firstName"
                type="text"
                placeholder="Enter your first name"
            />
        </div>

        <div class="form-group">
            <label for="lastName">Last Name</label>
            <input
                id="lastName"
                type="text"
                placeholder="Enter your last name"
            />
        </div>

        <div class="form-group">
            <label for="email">Email</label>
            <input
                id="email"
                type="email"
                placeholder="Enter your email"
            />
        </div>

        <div class="form-group">
            <label for="password">Password</label>
            <input
                id="password"
                type="password"
                placeholder="Enter your password"
            />
        </div>

        <button type="submit" class="submit-button">Submit</button>
    </form>

    <!-- TODO: Add success message section here -->
</div>

<style>
    .form-container {
        max-width: 480px;
        margin: 0 auto;
        padding: 2rem;
        background-color: white;
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }

    .form-group {
        margin-bottom: 1.5rem;
    }

    label {
        display: block;
        margin-bottom: 0.5rem;
        font-weight: 500;
        color: #374151;
    }

    input {
        width: 100%;
        padding: 0.75rem;
        border: 1px solid #D1D5DB;
        border-radius: 6px;
        font-size: 1rem;
        transition: border-color 0.15s ease-in-out;
    }

    input:focus {
        outline: none;
        border-color: #3B82F6;
        box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
    }

    input::placeholder {
        color: #9CA3AF;
    }

    input.error {
        border-color: #EF4444;
    }

    .error-message {
        display: block;
        margin-top: 0.5rem;
        font-size: 0.875rem;
        color: #EF4444;
    }

    .submit-button {
        width: 100%;
        padding: 0.75rem 1.5rem;
        background-color: #3B82F6;
        color: white;
        border: none;
        border-radius: 6px;
        font-size: 1rem;
        font-weight: 500;
        cursor: pointer;
        transition: background-color 0.15s ease-in-out;
    }

    .submit-button:hover {
        background-color: #2563EB;
    }

    .submit-button:focus {
        outline: none;
        box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.5);
    }

    .submit-button:disabled {
        background-color: #9CA3AF;
        cursor: not-allowed;
    }

    .success-message {
        margin-top: 1.5rem;
        padding: 1rem;
        background-color: #EDF7ED;
        border: 1px solid #C8E6C9;
        border-radius: 6px;
        color: #1B5E20;
    }
</style>