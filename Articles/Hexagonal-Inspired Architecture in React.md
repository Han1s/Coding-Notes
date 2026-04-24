https://alexkondov.com/hexagonal-inspired-architecture-in-react/

tldr; use hooks as ports to business logic.

>If you employ the strategy of decoupling your business logic from the rest of your application, you will gain the long-term advantage of being able to modify and replace it independently.

- components should be separated from the fetch logic
	- they should only show data and trigger events, not call apis etc.
		- the more interconnected they are, the harder it is to test independently
	- move as much of the domain functionality as you can outside the component

e.g. in the first iteration the component might look like this:
```tsx
function PostPage({ postId }) {
  const user = useUser()
  const [post, setPost] = useState(null)
  const [error, setError] = useState(null)

  const getPost = () => {
    axios
      .get(`http://example.com/api/v1/post/${postId}`)
      .then(setPost)
      .catch(setError)
  }

  const bookmarkPost = () => {
    axios.post(`http://example.com/api/v1/bookmark`, {
      data: { post_id: postId, user_id: userId },
    })
  }

  const reactToPost = (reaction) => {
    axios.post(`http://example.com/api/v1/reaction`, {
      data: { post_id: postId, user_id: userId, reaction },
    })
  }

  useEffect(() => {
    getPost()
  }, [])

  // Calculate total number of reactions for each type to display them
  const reactions = post?.user_reactions.reduce((acc, curr) => {
    if (!acc[curr.type]) {
      acc[curr.type] = 0
    }

    acc[curr.type] += 1
    return acc
  }, {})

  if (!post) {
    return <div>Loading</div>
  }

  if (error) {
    return <div>Error: {error.message} </div>
  }

  return (
    <div>
      <h1>{post?.title}</h1>
      <div>
        <p>{post?.text}</p>
      </div>
      <aside>
        <h3>Reactions</h3>
        <ul>
          {Object.entries(reactions).map(([type, count]) => (
            <li>
              <a onClick={() => reactToPost(type)}>
                {count} <ReactionEmoji type={type} />
              </a>
            </li>
          ))}
        </ul>
      </aside>
      <button onClick={bookmarkPost}>Bookmark</button>
    </div>
  )
}
```

in the second iteration we might abstract the business logic (the db call)
```tsx
function PostPage({ postId }) {
  const { post, error, bookmarkPost, reactToPost } = usePost(postId)

  if (!post) {
    return null
  }

  if (error) {
    return <div>Error: {error.message}</div>
  }

  return (
    <div>
      <h1>{post.title}</h1>
      <div>
        <p>{post.text}</p>
      </div>
      <aside>
        <h3>Reactions</h3>
        <ul>
          {Object.entries(post.reactions).map(([type, count]) => (
            <a onClick={() => reactToPost(type)}>
              {count} <ReactionEmoji type={type} />
            </a>
          ))}
        </ul>
      </aside>
      <button onClick={bookmarkPost}>Bookmark</button>
    </div>
  )
}
```

but we can go one step further and decouple the logic from the hooks as well
```tsx
function usePost(postId) {
  const user = useUser()
  const [post, setPost] = useState(null)
  const [error, setError] = useState(null)

  const getPost = () => {
    client.getPost(postId).then(setPost).catch(setError)
  }

  const bookmarkPost = () => {
    client.bookmarkPost(postId, userId)
  }

  const reactToPost = (reaction) => {
    client.storePostReaction(postId, userId, reaction)
  }

  useEffect(() => {
    getPost()
  }, [])

  return {
    post: mapToDomainObject(post),
    error,
    bookmarkPost,
    reactToPost,
  }
}
```

now the function is unaware of the environment. This is how to write the logic.
