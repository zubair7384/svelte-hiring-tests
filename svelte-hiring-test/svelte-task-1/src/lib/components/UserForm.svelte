<script lang="ts">
    import {writable} from "svelte/store"
    // TODO: Implement form state management
    const initialData = {
                    firstName: "",
                    lastName: "",
                    email: "",
                    password: "",
                }
    const formDetails = writable<App.UserFormData>(initialData)

    const success = writable<string | null>(null);
    const formErrors = writable<App.FormErrors>({})
    const submittedFormData = writable<Array<Omit<App.UserFormData, "password">>>([])
   
    // TODO: Implement form validation
    function validateForm(data: App.UserFormData): App.FormErrors {
        const err : App.FormErrors = {};

        if(!data.firstName.trim()) err.firstName = "First name is required";
        if(!data.lastName.trim()) err.lastName = "Last name is required";
        if(!data.email.trim()) err.email = "Email is required";
        if(!data.password.trim()) err.password = "Password is required";

        if (data.password.length < 6)
        err.password = "Password must be at least 6 characters"
    return err
    }
    // TODO: Implement submit handler

    function handleSubmit(e:Event) {
        e.preventDefault()

        formDetails.update((data) => {
            // console.log(data, "data")
            const error = validateForm(data);
            formErrors.set(error);

            if (Object.keys(error).length === 0) {
                success.set("Form details submitted successfully!")

                submittedFormData.update((entries) => [
                    ...entries,
                    {firstName: data.firstName, lastName: data.lastName, email: data.email},
                ])

                formDetails.set(initialData)
            } else {
                success.set(null)
            }
            return {...data}
        })

    }

    function handleInputChange() {
        success.set(null)
    }

    function handleClear() {
        formDetails.set(initialData)
        formErrors.set({});
        success.set(null)
    }

    // TODO: Implement success state management
</script>

<div class="form-container">
    <form on:submit={handleSubmit}>
        <div class="form-group">
            <label for="firstName">First Name</label>
            <input
                id="firstName"
                type="text"
                placeholder="Enter your first name"
                class:input-error={$formErrors.firstName}
                bind:value={$formDetails.firstName}
                on:input={handleInputChange}
            />
            {#if $formErrors.firstName}
            <span class="error-message">
                {$formErrors.firstName}
            </span>
            {/if}
        </div>

        <div class="form-group">
            <label for="lastName">Last Name</label>
            <input
                id="lastName"
                type="text"
                placeholder="Enter your last name"
                class:input-error={$formErrors.lastName}
                bind:value={$formDetails.lastName}
                on:input={handleInputChange}
            />
            {#if $formErrors.lastName}
            <span class="error-message">
                {$formErrors.lastName}
            </span>
            {/if}
        </div>

        <div class="form-group">
            <label for="email">Email</label>
            <input
                id="email"
                type="email"
                placeholder="Enter your email"
                class:input-error={$formErrors.email}
                bind:value={$formDetails.email}
                on:input={handleInputChange}
            />
            {#if $formErrors.email}
            <span class="error-message">
                {$formErrors.email}
            </span>
            {/if}
        </div>

        <div class="form-group">
            <label for="password">Password</label>
            <input
                id="password"
                type="password"
                placeholder="Enter your password"
                class:input-error={$formErrors.password}
                bind:value={$formDetails.password}
                on:input={handleInputChange}
            />
            {#if $formErrors.password}
            <span class="error-message">
                {$formErrors.password}
            </span>
            {/if}
        </div>
<div class="form-buttons">
    <button type="submit" class="submit-button">Submit</button>
    <button type="button" class="clear-button" on:click={handleClear}>Clear</button>
</div>
    </form>

    <!-- TODO: Add success message section here -->
     {#if $success} 
     <div class="success-message">{$success}</div>
     {/if}
{#if $submittedFormData.length > 0}
    <table class="data-table-wrapper">
        <thead>
            <tr>
                <th>First Name</th>
                <th>Last Name</th>
                <th>Email</th>
            </tr>
        </thead>
        <tbody>
        {#each $submittedFormData as entries}
            <tr>
                <td>{entries.firstName}</td>
                <td>{entries.lastName}</td>
                <td>{entries.email}</td>
            </tr>
            {/each}
        </tbody>
    </table>
    {/if}
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

    .form-buttons {
        display: flex;
        align-items: center;
        gap: 10px;
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
    .clear-button {
        padding: 0.75rem 1.5rem;
        background-color: #fff;
        color: #3B82F6;
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
    .clear-button:hover {
        background-color: #eeeeee;
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
    .data-table-wrapper {
        margin-top: 1.5rem;
        width: 100%;
        border: collapse;
    }
    .data-table-wrapper th,
    .data-table-wrapper td {
        padding: 1rem;
        border: 1px solid #d9d9d9;
        text-align: left;
    }

    .data-table-wrapper td {
        font-weight:600 ;
    }
</style>