<script setup>
import useTaskCompose from '@/composables/useTaskCompose.js'
const { deleting, deleteTask, updateFieldByCurrentTask } = useTaskCompose()

const props = defineProps({
    text: { required: true },
    dueDate: {},
    currentTaskData: {},
    updateTasksData: {},
    task: {},
    insertNewOn:{}
})

const deleteTaskAndUpdate = async (task) => {
    updateFieldByCurrentTask(task)
    await deleteTask()
    props.updateTasksData({}, task.id, true)
}
</script>
<template>


    <div
        class="w-full p-1  flex flex-row   bg-white border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700">
        <div class="flex w-full  flex-col items-start   ">
            <span class="  overflow-hidden text-sm px-4 pb-4 text-gray-500 dark:text-gray-400">{{
                props.text }}</span>
            <div class="px-4 flex w-full justify-between ">
                <div>
                    <div class="cursor-default inline-flex items-center px-2 py-1 text-xs font-medium text-center text-white bg-orange-300 rounded-lg hover:bg-orange-500 "
                        :class="props.dueDate ? '' : 'hidden'">{{ props.dueDate ?? '--' }}</div>
                </div>
                <div v-if="!deleting" class="flex gap-3">
                    <svg @click="() => deleteTaskAndUpdate(props.task)" xmlns="http://www.w3.org/2000/svg" fill="none"
                        viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="cursor-pointer w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round"
                            d="m14.74 9-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 0 1-2.244 2.077H8.084a2.25 2.25 0 0 1-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 0 0-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 0 1 3.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 0 0-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 0 0-7.5 0" />
                    </svg>
                    <svg @click="() => props.insertNewOn(props.task)" xmlns="http://www.w3.org/2000/svg" fill="none"
                        viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="cursor-pointer  w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round"
                            d="m16.862 4.487 1.687-1.688a1.875 1.875 0 1 1 2.652 2.652L10.582 16.07a4.5 4.5 0 0 1-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 0 1 1.13-1.897l8.932-8.931Zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0 1 15.75 21H5.25A2.25 2.25 0 0 1 3 18.75V8.25A2.25 2.25 0 0 1 5.25 6H10" />
                    </svg>

                </div>
                <div v-else>
                    <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24">
                        <circle cx="4" cy="12" r="3" fill="currentColor">
                            <animate id="svgSpinners3DotsFade0" fill="freeze" attributeName="opacity"
                                begin="0;svgSpinners3DotsFade1.end-0.25s" dur="0.75s" values="1;0.2" />
                        </circle>
                        <circle cx="12" cy="12" r="3" fill="currentColor" opacity="0.4">
                            <animate fill="freeze" attributeName="opacity" begin="svgSpinners3DotsFade0.begin+0.15s"
                                dur="0.75s" values="1;0.2" />
                        </circle>
                        <circle cx="20" cy="12" r="3" fill="currentColor" opacity="0.3">
                            <animate id="svgSpinners3DotsFade1" fill="freeze" attributeName="opacity"
                                begin="svgSpinners3DotsFade0.begin+0.3s" dur="0.75s" values="1;0.2" />
                        </circle>
                    </svg>
                </div>
            </div>
        </div>

    </div>

</template>