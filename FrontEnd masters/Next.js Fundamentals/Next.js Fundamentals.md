https://master.dev/courses/next-js-v4/course-project-setup/

regular setup:
- visit https://neon.new/database/019f945f-be97-7718-bf9a-4a56d5d2cc97 and create db
- copy link to .env
- run `npm run db:push`

- Layouts
	- if you want the layout to change swap it with `template.tsx`. This is useful with animations for example. Templates are not persistent.

- groups
	- they are just subpaths that are not visible in the UI. Good for sharing layouts, etc.¬

## Server actions
- more streamlined way to create API routes
- its basically the same thing as API routes
	- you should not use API routes, instead use server action
- frequently used with forms
- its basically a clean syntax for creating API route
	- you can also create them to GET instead of POST
- you are basically making a http request but not writing a code to make a http request

```jsx
'use server'  
  
import { z } from 'zod'  
import {  
  verifyPassword,  
  createSession,  
  createUser,  
  deleteSession,  
} from '@/lib/auth'  
import { getUserByEmail } from '@/lib/dal'  
import { mockDelay } from '@/lib/utils'  
import { redirect } from 'next/navigation'  
  
// Define Zod schema for signin validation  
const SignInSchema = z.object({  
  email: z.string().min(1, 'Email is required').email('Invalid email format'),  
  password: z.string().min(1, 'Password is required'),  
})  
  
// Define Zod schema for signup validation  
const SignUpSchema = z  
  .object({  
    email: z.string().min(1, 'Email is required').email('Invalid email format'),  
    password: z.string().min(6, 'Password must be at least 6 characters'),  
    confirmPassword: z.string().min(1, 'Please confirm your password'),  
  })  
  .refine((data) => data.password === data.confirmPassword, {  
    message: "Passwords don't match",  
    path: ['confirmPassword'],  
  })  
  
export type SignInData = z.infer<typeof SignInSchema>  
export type SignUpData = z.infer<typeof SignUpSchema>  
  
export type ActionResponse = {  
  success: boolean  
  message: string  
  errors?: Record<string, string[]>  
  error?: string  
}  
  
export const signin = async (formData: FormData): Promise<ActionResponse> => {  
  await mockDelay(1000);  
  
  const data = {  
    email: formData.get('email') as string,  
    password: formData.get('password') as string,  
  }  
  
  const validationResult = SignInSchema.safeParse(data);  
  try {  
    if (!validationResult.success) {  
      return {  
        success: false,  
        message: "Validation failed",  
        errors: validationResult.error.flatten().fieldErrors  
      }  
    }  
  
    const user = await getUserByEmail(data.email);  
    if (!user) {  
      return {  
        success: false,  
        message: "Invalid email or password",  
        errors: {  
          email: ["invalid email or password"]  
        }  
      }  
    }  
  
    const isPasswordValid = await verifyPassword(data.password, user.password)  
  
    if (!isPasswordValid) {  
      return {  
        success: false,  
        message: "Invalid email or password",  
        errors: {  
          email: ["invalid email or password"]  
        }  
      }  
    }  
  
    await createSession(user.id);  
    return {  
      success: true,  
      message: "Signed in successfully",  
    }  
  } catch (error) {  
    console.error(error)  
    return {  
      success: false,  
      message: 'Something bad happened',  
      error: 'Something bad happened',  
    }  
  }  
}  
  
export const signup = async (formData: FormData) => {  
  try {  
  const data = {  
    email: formData.get('email') as string,  
    password: formData.get('password') as string,  
    confirmPassword: formData.get('confirmPassword') as string,  
  }  
  
  const validationResult = SignUpSchema.safeParse(data);  
  
  if (!validationResult.success) {  
    return {  
      success: false,  
      message: "Validation Failed",  
      errors: validationResult.error.flatten().fieldErrors,  
    }  
  }  
  
  const existingUser = await getUserByEmail(data.email);  
  if (existingUser) {  
    return {  
      success: false,  
      message: 'You already have an account',  
      errors: ['You already have an account'],  
    }  
  }  
  
  const user = await createUser(data.email, data.password);  
  if (!user) {  
    return {  
      success: false,  
      message: "try again",  
      errors: ['Account could not be created']  
    };  
  }  
  
  await createSession(user.id);  
  
  return {  
    success: true,  
    message: "Account created successfully",  
  }} catch (e) {  
    console.error(e);  
    return {  
      success: false,  
      message: 'Something bad happened',  
      error: 'Something bad happened',  
    }  
  }  
}  
  
export const signout = async () => {  
  try {  
    await deleteSession();  
  } catch (e) {  
    console.error(e);  
  } finally {  
    redirect('/signin');  
  }  
}
```

## Authentication
- Push all the data as much down as possible
	- 'use cache' when the data are static
	- use suspense when the data are dynamic
